`Android Graphics Pipeline: ��Button��Framebuffer (Part 1)`
---

>
* ԭ������ : [Android Graphics Pipeline: From Button to Framebuffer (Part 1)](https://blog.inovex.de/android-graphics-pipeline-from-button-to-framebuffer-part-1/)
* ���� : [dupengwei](https://github.com/dupengwei) 
* У����: [����У���ߵ�github�û���](github����)  
* ״̬ :  δ��� / У���� / ��� 

In this mini-series of blog articles we want to shed some light on the internals of the Android Graphics Pipeline. Google itself already released some insights and documentation on the subject such as the beautiful Google I/O 2012 talk For Butter or Worse by Chet Haase and Romain Guy (go watch it if you haven��t!) or the article Graphics architecture. While they certainly help to get the big picture involved in getting a simple view displayed on the screen, they are not that helpful when trying to understand the source code behind it. This series will give you a gentle jump start into the interesting world of the Android Graphics Pipeline.

�����С�Ͳ���ϵ���������������Ȥ�о� Android Graphics Pipeline �ڲ��ṹ�Ŀ����ߴ���һЩ�������ڴ������ϣ�Google�Լ�Ҳ������һЩ������ĵ�������Chet Haase �� Romain Guy���ֵ�Google I/O 2012�ݽ�[For Butter or Worse](https://www.youtube.com/watch?v=Q8m9sHdyXnE) (���û������ȥ������!) ������ [Graphics architecture](http://source.android.com/devices/graphics/architecture.html) ����Ȼ��Щ���Ͽ϶��ܰ������ǴӺ�������һ���򵥵�view�������ʾ����Ļ�ϣ����ǵ����ǳ���ȥ��ⱳ���Դ����ʱ����Щ�����ǵİ��������󡣱�ϵ�в��Ľ������߽�Android Graphics Pipeline�����Ȥ�����硣

Beware, a lot of source code and sequence diagrams will be involved in this mini-series! Its worth a read though, especially if you have even the slightest interest in the Android Graphics Pipeline, as you are going to learn a lot (or at least get to look at some pretty pictures). So get yourself a coffee and read on!

��ע�⣬��С��ϵ�в����л��漰������Դ���������ͼ����ֵ��һ�����������Android Graphics Pipelineһ����ȤҲû�У���Ҳ����ѧ���ܶࣨ���������ٿ�����ЩƯ����ͼƬ�������Ը��Լ�һ�����ȣ����ɣ�

## Introduction

## ����

In order to fully understand the journey all views undertake on the way to the screen, we will use a small demo app and describe every major stage in the Android Graphics Pipeline, starting with the public Android Java API (SDK), going to native C++ code and finally looking at the raw OpenGL drawing operations.

Ϊ�˳�����view��ʾ����Ļ�Ĺ��̣����ǲ���һ��СDemo������Android Graphics Pipeline��ÿ����Ҫ�׶Σ���Android Java API (SDK)��ʼ��Ȼ���Ǳ���C++���룬���ԭʼ��OpenGL��ͼ������

![one-button-layout-cropped](one-button-layout-cropped-300x186.png)

The demo app in all its glory. This little app is causing enough code-coverage in the Android Graphics internals, so that it��s actually a pretty good example.

���Demo���൱�Ĺ�ʶ�Ŀ�����СС��app�� Android Graphics���ڲ��ṹ��������Ĵ��븲�ǣ����ԣ���ʵ������һ���൱�õ����ӡ�

The activity consists of a simple RelativeLayout, an ActionBar with the application icon and title and a simple Button which reads Hello world!.

���activity��һ����RelativeLayout��һ����Ӧ��ͼ��ͱ���ActionBar ��һ��������Hello world!���ļ�Button��ɡ�

![one-button-viewhierarchy](one-button-viewhierarchy-1024x396.png)

The view hierarchy of our simple demo app is actually quite complex.

��������򵥵�Demo����ͼ��ʵ�������൱���ӵġ�

Inside the Android view hierarchy, the relative layout consists of a simple color-gradient background. More complex, the action bar is composed of the background, which is a gradient combined with a bitmap, the One Button text element and the application icon, which is also a bitmap. A 9-Patch is used as the background for the button, and the text element Hello World! is drawn on top of it. The navigation bar and status bar at the top and bottom of the screen are not part of the apps activity, they will be rendered by the  SystemUI  system service instead.

��Android ��ͼ���ڲ�����Բ��֣�relative layout����һ���򵥵���ɫ���䱳����ɡ������ӵģ�action bar��һ������ı������һ��bitmap��**One Button**�ı�Ԫ�غ�Ӧ��ͼ�꣨Ҳ��һ��bitmap����ɡ�9-Patch������ť�ı������ı�**Hello World!**�����������ϲ㡣��Ļ�����ĵ������͵ײ���״̬��������app��activity���֣�������ϵͳ����`SystemUI`������Ⱦ��

## The Big Picture: Pipeline Overview

## ���������Pipeline����

Having watched the Google I/O talk For Butter or Worse, you will certainly recognize the following slide, which shows the complete Android Graphics Pipeline.

����Google I/O�ݽ�**For Butter or Worse**����϶���ʶ����Ļõ�Ƭ������ʾ��������Android Graphics Pipeline��

![pipeline](pipeline-1024x458.png)

The complete Android Graphics Pipeline, as presented at Google I/O 2012.

��Google I/O 2012�ݽ����ṩ��������Android Graphics Pipeline��

The Surface Flinger is responsible for creating a graphics buffer and compositing it onto the main display and while certainly very important for the Android system, is not covered at this time.

Surface Flinger���𴴽�ͼ�λ�����������ϳɵ�����ʾ������Ȼ���Ӧ��׿ϵͳ�ǳ���Ҫ�������ڴ˲������ǡ�

Instead, we will look at a fine selection of components which are doing most of the heavy lifting in bringing the view to the screen:

�෴�������������ж��ֿɹ�ѡ����������Щ������ž�������Ĺ�����view��ʾ����Ļ��

![interesting_bits](interesting_bits-1024x302.png)

The interesting bits (at least for these blog posts) of the pipeline.



## Display Lists

As you may already know, Android uses a concept called DisplayLists to render all its views. For those of you who don��t know, a display list is a sequence of graphics commands needed to be executed to render a specific view. These display lists are an important element to achieve the high performance of the Android Graphics Pipeline.

����������Ѿ�֪����Android ʹ��һ������DisplayLists�ĸ���ȥ��Ⱦ���е�view�����ڲ�֪��������˵��display list��һ����ͼ�������м��ϣ���Ҫִ����Щ����ȥ��Ⱦָ����view��display lists��Android Graphics Pipeline�ﵽ�����ܵ���ҪԪ�ء�

![display-lists](display-lists.png)

Every view of the view hierarchy has a corrsponding display list, which is generated by the views onDraw() method, which every developer knows about. In order to draw the view hierarchy onto the screen, only the display lists need to be evaluated and executed. In case a single view gets invalidated (due to user input, animations or transitions), the affected display lists will be rebuilt and eventually redrawn. This is preventing Android from calling the quite expensive onDraw() methods every frame.

ÿ����ͼ���view�������Ӧ��display list��ÿ�������߶�֪��`onDraw()`���������display list������view��`onDraw()`�������ɵġ�Ϊ�˽���ͼ�㻭����Ļ�ϣ�ֻ��display lists��Ҫ��������ִ�С�����ĳ����һviewʧЧ�����û����롢������ת��������Ӱ���display lists�����ؽ����ػ档��ͱ���Android��ÿ��frame������൱�ķ���Դ��`onDraw()`��

Display lists can also be nested, meaning that a display list can issue a command to draw a childrens display list. This is important in order to be able to reproduce view hierarchies with display lists. After all, even our simple app has multiple nested views.

Display lists Ҳ���Ա�Ƕ�ף�����ζ��һ��Display listҲ���Է���һ���������һ����display list����Ը�����ͼ���display lists��˵�ǳ���Ҫ���Ͼ�����ʹ���ǵļ�appҲ���ж��Ƕ����ͼ��

These commands are a mixture of statements that can be directly mapped to OpenGL commands, such as translating and setting up clipping rectangles, and more complex commands such as DrawText and DrawPatch. These need a more complex set of OpenGL commands.

��Щ��������Ŀ���ֱ��ӳ�䵽OpenGL����緭������ü������󣬻�����ӵ�������`DrawText` �� `DrawPatch`����Щ������Ҫ�����ӵ�OpenGL�����

`An example of a display list for a button.`

`һ����ť��display listʾ��`

```java
Save 3
DrawPatch
Save 3
ClipRect 20.00, 4.00, 99.00, 44.00, 1
Translate 20.00, 12.00
DrawText 9, 18, 9, 0.00, 19.00, 0x17e898
Restore
RestoreToCount 0
```

In the example above, you can clearly see what kind of operations are present in a display list for our simple button. The first operation is to save the current translation matrix to the stack, so that it can be later restored. It then proceeds to draw the buttons 9-Patch, followed by another save command. This is necessary because for the text to be drawn, a clipping rectangle is set up to only affect the region that where text will be drawn. Mobile GPUs can take this rectangle as an hint to further optimize the draw calls in later stages. The drawing origin is than translated to the text position and the text is drawn. At the end, the original translation matrix and state is restored from the stack, which also resets the clipping rectangle.

�������ʾ���У����������ؿ���һ���򵥵İ�ť(���ƹ��̣�display list�ṩ��ʲô���Ĳ�������һ�������Ǳ��浱ǰ�������ջ�У�����������Իָ���Ȼ���ֻ���9-Patch��ť��������������һ������������Ǳ�Ҫ�ģ���Ϊ����Ҫ���Ƶ��ı���˵��ֻ�л����ı�������Żᴴ���ü������ֻ���ͼ���������˾���������һ�������Ա��ں����׶ζԻ�ͼ���ý�һ���Ż���Ȼ�󽫻滭Բ��ת�����ı�λ�ã��������ı�����������ת�������״̬�Ӷ��л�ԭ���ü�����Ҳ�����á�

The complete log of the display lists for our example application can be seen at the bottom of this post.

����ƪ���µĵײ����Կ���ʾ���õĵ�display lists��������־��

## Diving into code

## �������

With this newly accuired knowledge we are ready to dive into the code.

������Щ�»�ȡ��֪ʶ������׼��������롣

### Root View

### ����ͼ��Root View��

Every Android activity has an implicit root view at the top of the view hierarchy, containing exactly one child view. This child is the first real view of the application defined by the application developer. The root view is responsible for scheduling and executing multiple operations such as drawing and invalidating views, among other.

ÿ��Android activity����ͼ�����㶼��һ����ʽ����ͼ��Root View��������һ����view�������view�ǳ���Ա��Ӧ���ж���ĵ�һ��������view������ͼ������Ⱥ�ִ�ж��֣����ͼ��ʹview��Ч�ȵȡ�

Similarly, every view has a reference to its parent. The first view inside the view hierarchy, which the root view references, has this root view as a parent. While serving as a base class for every visible element and widget, the View class does not support any children. However, the derrived ViewGroup supports multiple children and serves as a container base class, which is used by the standard layouts ( RelativeLayout etc.).

���Ƶģ�ÿ��view����һ��parent�����á���ͼ���ڲ��ĵ�һ��view������ͼ��Ϊparent����ȻView����Ϊÿ�����ӻ���Ԫ�ػ�����Ļ��࣬����������֧���κ����ࡣȻ������������ViewGroup֧�ֶ����࣬����Ϊһ���������࣬���Ѿ�����׼���֣�RelativeLayout �ȵ�)�����á�

If a view is (partially) invalidated, the view will call the root views invalidateChildInParent() method. The root view keeps track of all invalidated areas and schedules a new traversal at the choreographer, which is performed on the next VSync event.

���һ��view�ֲ��ػ棬��ô��view����ø���ͼ��invalidateChildInParent()����������ͼ���������ػ�����򣬲���choreographer����һ���µı�����choreographer������һ��VSync�¼�ִ�С�

![view-invalidate](view-invalidate.png)

ViewRoot: InvalidateChildInParent(��)

```java
public ViewParent invalidateChildInParent(int[] location, Rect dirty) {
    // Add the new dirty rect to the current one
    mDirty.union(dirty.left, dirty.top, 
                 dirty.right, dirty.bottom);
    // Already scheduled?
    if (!mWillDrawSoon) {
        scheduleTraversals();
    }
    return null;
}
```

## Creating the Display Lists

## ����Display Lists

As previously mentioned, each view is responsible to generate its own display list. When a VSync event is fired and the choreographer called performTraversals on the root view, the  HardwareRenderer is asked to draw the view, which in turn will ask the view to generate its display list.

����֮ǰ�ᵽ�ģ�ÿ��view���������Լ���display list����һ��VSync�¼���������choreographer���ø���ͼ��`performTraversals`����������ͼҪ��`HardwareRenderer`����view��`HardwareRenderer`������Ҫ��view�����Լ���display list��

![perform-traversals1](perform-traversals1.png)

With currently almost 20.000 lines of code, the View  is one of the bigger classes inside the Android framework. This comes as no surprise, as it is the building block for every widget and application. It handles the keyboard, trackball and touch events, as well as scrolling, scrollbars, layouting and measuring, and much, much more.

��Android framework���У�View������һ���Ƚϴ���࣬��ǰ����������20000�С��Ⲣ�����˾��棬��Ϊ����ÿ��С�����Ӧ�õĹ����顣��������̡��켣�򡢴����¼�,�Լ�����,������,���ֺͲ���,���кܶ�ܶࡣ

![view-getdisplaylist](view-getdisplaylist.png)


Called by the Hardware Renderer, the View.getDisplayList(��) method will create a new internal display list, which will be used for rest of the views lifetime. The internal display list is then asked to supply a canvas big enough to accommodate the view. Supplying a  GLES20RecordingCanvas, the view and all its children will use it to draw upon, and is therefore handed to the  draw(��) method. The canvas is somewhat special, as it will not execute drawing commands but rather save them as commands inside the display list. This means that the widgets and every view can use the normal drawing API without even noticing that the commands are rendered to a display list.

`View.getDisplayList(��)`������Hardware Renderer����ʱ���ᴴ��һ���ڲ���display list������ڲ�display list������view�������ڵ�ʣ�ಿ�ű�ʹ�á�Ȼ������ڲ�display list��Ҫ���ṩһ���㹻��Ļ������������view���ṩһ��GLES20RecordingCanvas������view������children�����������ͼ�������ݸ�`draw(��)`��������������е����⣬��Ϊ����ִ�л�ͼ������Ǳ������display list������ζ��С�����ÿ��view��ʹ�������Ļ�ͼAPI�����������עdisplay list�ڲ�������

`View: getDisplayList(��)`
```java
private DisplayList getDisplayList(DisplayList displayList, 
                                   boolean isLayer) {
    HardwareCanvas canvas = displayList.start(width, height);
    if (!isLayer && layerType != LAYER_TYPE_NONE) {
        // Layers don't get drawn via a display list
    } else {
        draw(canvas);
    }
    return displayList;
}
```

Inside the draw(��) method, the view will execute the onDraw() code, rendering itself onto the supplied canvas. If the view has any children, it will also call the draw() method of each of them. These children could be anything, from a normal button to another layout or view group, which itself includes another set of children, which will also get drawn.

��`draw(��)`�����У�view��ִ��`onDraw()`�����Ĵ��룬��Ⱦ�Լ��������ϡ�������view���κ�children��children���Ե���`draw()`��������Щchildren�������κζ�����������һ�������İ�ť��Ҳ������һ�����ֻ�view group����Щchildren���������children�����������ơ�

![view-draw](view-draw.png)


## Read on

## ��������ȥ

With the generation of the display list this first part comes to an end. Jump to part 2 where we will actually take a look at how these display lists get rendered to the screen!

������display list�Ĳ�������һ���ֽ����ˡ���ת����2����,���ǻῴ����Щdisplay lists��γ�������Ļ��!

## Download

## ����

The full Bachelor��s Thesis on which this article is based is available for download.

���Ĳο�������ѧʿ���Ŀɹ�[����](http://mathias-garbe.de/files/introduction-android-graphics.pdf)





