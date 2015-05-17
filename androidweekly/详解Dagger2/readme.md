���Dagger2
---

> * ԭ������ : [Tasting Dagger 2 on Android](http://fernandocejas.com/2015/04/11/tasting-dagger-2-on-android/)
* ԭ������ : [Fernando Cejas](http://fernandocejas.com/)
* [���ĳ��� :  ��������ǰ�� www.devtf.cn](http://www.devtf.cn)
* ���� : [xianjiajun](https://github.com/xianjiajun) 
* У����: [����У���ߵ�github�û���](github����)  
* ״̬ :  У����

Why dependency injection?
The first (and indeed most important) thing we should know about it is that has been there for a long time and uses Inversion of Control principle, which basically states that the flow of your application depends on the object graph that is built up during program execution, and such a dynamic flow is made possible by object interactions being defined through abstractions. This run-time binding is achieved by mechanisms such as dependency injection or a service locator.
##Ϊʲôʹ������ע��
����������Ҫ֪���������ںܳ���һ��ʱ���ﶼ�����ÿ��Ʒ�תԭ��涨��Ӧ�ó��������ȡ�����ڳ�������ʱ����ͼ�Ľ�����ͨ��������Ķ��󽻻�����ʵ�������Ķ�̬���̡���ʹ������ע�뼼�����߷���λ��������������ʱ�󶨡�

Said that we can get to the conclusion that dependency injection brings us important benefits:

Since dependencies can be injected and configured externally we can reuse those components.
When injecting abstractions as collaborators, we can just change the implementation of any object without having to make a lot of changes in our codebase, since that object instantiation resides in one place isolated and decoupled.
Dependencies can be injected into a component: it is possible to inject mock implementations of these dependencies which makes testing easier.

ʹ������ע����Դ������ºô���

* ������ע������ö��������֮�⡣
* ��Ϊ��������һ������������ϵĵط���ʼ�������Ե�ע����󷽷���ʱ������ֻ��Ҫ�޸Ķ����ʵ�ַ����������ô�Ĵ���⡣
* ��������ע�뵽һ������У����ǿ���ע����Щ������ģ��ʵ�֣�����ʹ�ò��Ը��Ӽ򵥡�

One thing that we will see is that we can manage the scope of our instances created, which is something really cool and from my point of view, any object or collaborator in your app should not know anything about instances creation and lifecycle and this should be managed by our dependency injection framework.
���Կ������ܹ�������ʵ���ķ�Χ��һ���ǳ��������顣���ҵĹ۵㣬��app�е����ж������Э���߶���Ӧ��֪���й�ʵ���������������ڵ��κ����飬��Щ��Ӧ�������ǵ�����ע���ܹ���ġ�

![p1](http://fernandocejas.com/wp-content/uploads/2015/04/dependency_inversion1.png)

What is JSR-330?
Basically dependency injection for Java defines a standard set of annotations (and one interface) for use on injectable classes in order to to maximize reusability, testability and maintainability of java code.
Both Dagger 1 and 2 (also Guice) are based on this standard which brings consistency and an standard way to do dependency injection.
#ʲô��JSR-330��
Ϊ�����̶ȵ���ߴ���ĸ����ԡ������Ժ�ά���ԣ�java������ע��Ϊע�����е�ʹ�ö�����һ����ע�⣨�ͽӿڣ���׼��Dagger1��Dagger2������Guice�����ǻ������ױ�׼��������������ȶ��Ժͱ�׼������ע�뷽����

Dagger 1
I will be very quick here because this version is out of the purpose of this article. Anyway, Dagger 1 has a lot to offer and I would say that nowadays is the most popular dependency injector used on Android. It has been created by Square inspired by Guice.

Its fundamentals are:

Multiple injection points: dependencies, being injected.
Multiple bindings: dependencies, being provided.
Multiple modules: a collection of bindings that implement a feature.
Multiple object graphs: a collection of modules that implement a scope.
Dagger 1 uses compile time to figure out bindings but also uses reflection, and although it is not used to instantiate objects, it is used for graph composition. All this process happens at runtime, where Dagger tries to figure out how everything fits together, so there is a price to pay: inefficiency sometimes and difficulties when debugging.
#Dagger1
����汾������ƪ���µ��ص㣬������ֻ�Ǽ��Ե�˵һ�¡�����������Dagger1�������˺ܶ�Ĺ��ף�����˵�����Android�������е�����ע���ܡ�������Square��˾�ܵ�Guice���������ġ�

�����ص㣺

* ���ע��㣺������ͨ��injected
* ���ְ󶨷�����������ͨ��provided
* ���modules��ʵ��ĳ�ֹ��ܵİ󶨼���
* �������ͼ�� ʵ��һ����Χ��modules����

Dagger1���ڱ����ʱ��ʵ�а󶨣�����Ҳ�õ��˷�����ơ���������䲻������ʵ��������ģ���������ͼ�Ĺ��ɡ�Dagger�������е�ʱ��ȥ����Ƿ�һ�ж���������������ʹ�õ�ʱ��Ḷ��һЩ���ۣ�ż������Ч�͵������ѡ�

Dagger 2
Dagger 2 is a fork from Dagger 1 under heavy development by Google, currently version 2.0. It was inspired by AutoValue project (https://github.com/google/auto, useful if you are tired of writing equals and hashcode methods everywhere).
From the beginning, the basic idea behind Dagger 2, was to make problems solvable by using code generation, hand written code, as if we were writing all the code that creates and provides our dependencies ourselves.
#Dagger2
Dagger2��Dagger1�ķ�֧���ɹȸ蹫˾���ֿ�����Ŀǰ�İ汾��2.0��Dagger2���ܵ�[AutoValue��Ŀ](https://github.com/google/auto)��������
�տ�ʼ��Dagger2�������Ļ���˼���ǣ��������ɺ�д�Ĵ����ϴﵽ�������еĲ������ṩ�����Ĵ��붼����д�����ӡ�

If we compare this version with its predecessor, both are quite similar in many aspects but there are also important differences that worth mentioning:
No reflection at all: graph validation, configurations and preconditions at compile time.
Easy debugging and fully traceable: entirely concrete call stack for provision and creation.
More performance: according to google they gained 13% of processor performance.
Code obfuscation: it uses method dispatch, like hand written code.
Of course all this cool features come with a price, which makes it less flexible: for instance, there is no dynamism due to the lack of reflection.

������ǽ�Dagger2��1�Ƚϣ����������ںܶ෽�涼�ǳ����ƣ���Ҳ�к���Ҫ���������£�

* ��Ҳû��ʹ�÷��䣺ͼ����֤�����ú�Ԥ�����ö��ڱ����ʱ��ִ�С�
* ���׵��ԺͿɸ��٣���ȫ����ص����ṩ�ʹ����Ķ�ջ
* ���õ����ܣ��ȸ��������������13%�Ĵ�������
* ���������ʹ�÷����ַ�������ͬ�Լ�д�Ĵ���һ��

��Ȼ������Щ�ܰ����ص㶼��Ҫ����һ�����ۣ��Ǿ���ȱ������ԡ�����˵��Dagger2����û�÷�������û�ж�̬���ơ�

Diving deeper
To understand Dagger 2 it is important (and probably a bit hard in the beginning) to know about the fundamentals of dependency injection and the concepts of each one of these guys (do not worry if you do not understand them yet, we will see examples):
@Inject: Basically with this annotation we request dependencies. In other words, you use it to tell Dagger that the annotated class or field wants to participate in dependency injection. Thus, Dagger will construct instances of this annotated classes and satisfy their dependencies.
@Module: Modules are classes whose methods provide dependencies, so we define a class and annotate it with @Module, thus, Dagger will know where to find the dependencies in order to satisfy them when constructing class instances. One important feature of modules is that they have been designed to be partitioned and composed together (for instance we will see that in our apps we can have multiple composed modules). 
@Provide: Inside modules we define methods containing this annotation which tells Dagger how we want to construct and provide those mentioned dependencies.
#�����о�
��Ҫ�˽�Dagger2���ͱ���Ҫ֪������ע��Ļ����������е�ÿһ�����

* @Inject: ͨ����������Ҫ�����ĵط�ע�⡣���仰˵������������Dagger�������߱���Ҫ�ӵ�����ע���С�������Dagger�ͻṹ��һ��������ʵ�����������ǵ�������
* @Module: Modules���ṩ�����������ࡣ���Ƕ���һ���࣬��@Moduleע�⣬����Dagger�ڹ������ʵ����ʱ�򣬾�֪��������ȥ�ҵ���Ҫ��������modules��һ����Ҫ���������Ǳ����Ϊ�ֿ��Ĳ������һ�𣨱���˵�������ǵ�app�п����ж�������һ���modules����
* @Provide: ��modules�У����Ƕ���ķ����������ע�⣬�Դ�������Dagger������Ҫ��������ṩ��Щ������

@Component: Components basically are injectors, let��s say a bridge between @Inject and @Module, which its main responsibility is to put both together. They just give you instances of all the types you defined, for example, we must annotate an interface with @Component and list all the @Modules that will compose that component, and if any of them is missing, we get errors at compile time. All the components are aware of the scope of dependencies it provides through its modules. 
@Scope: Scopes are very useful and Dagger 2 has has a more concrete way to do scoping through custom annotations. We will see an example later, but this is a very powerful feature, because as pointed out earlier, there is no need that every object knows about how to manage its own instances. An scope example would be a class with a custom @PerActivity annotation, so this object will live as long as our Activity is alive. In other words, we can define the granularity of your scopes (@PerFragment, @PerUser, etc). 
@Qualifier: We use this annotation when the type of class is insufficient to identify a dependency. For example in the case of Android, many times we need different types of context, so we might define a qualifier annotation ��@ForApplication�� and ��@ForActivity��, thus when injecting a context we can use those qualifiers to tell Dagger which type of context we want to be provided.

* @Component: Components�Ӹ�������˵����һ��ע������Ҳ����˵��@Inject��@Module��������������Ҫ���þ����������������֡�Components�����ṩ���ж����˵����͵�ʵ�������磺���Ǳ�����@Componentע��һ���ӿ�Ȼ���г����е�@Modules��ɸ���������ȱʧ���κ�һ�鶼���ڱ����ʱ�򱨴����е����������ͨ������modules֪�������ķ�Χ��
* @Scope: Scopes���Ƿǳ������ã�Dagger2����ͨ���Զ���ע���޶�ע�������򡣺������ʾһ�����ӣ�����һ���ǳ�ǿ����ص㣬��Ϊ����ǰ��˵��һ����û��Ҫ��ÿ������ȥ�˽���ι������ǵ�ʵ������scope�������У��������Զ����@PerActivityע��һ���࣬�������������ʱ��ͺ�activity��һ��������˵�������ǿ��Զ������з�Χ������(@PerFragment, @PerUser, �ȵ�)��
* Qualifier: ��������Ͳ����Լ���һ��������ʱ�����ǾͿ���ʹ�����ע���ʾ�����磺��Android�У����ǻ���Ҫ��ͬ���͵�context���������ǾͿ��Զ���qualifierע�⡰@ForApplication���͡�@ForActivity����������ע��һ��context��ʱ�����ǾͿ��Ը���Dagger������Ҫ�������͵�context��

Shut up and show me the code!
I guess it is too much theory for now, so let��s see Dagger 2 in action, although it is a good idea 
to first set it up by adding the dependencies in our build.gradle file:
#���ϻ��ϴ���
ǰ���Ѿ����˺ܶ������ˣ����Խ����������ǿ������ʹ��Dagger2�����Ȼ���Ҫ�����ǵ�build.gradle�ļ����������ã�
```java
apply plugin: 'com.neenbedankt.android-apt'
 
buildscript {
  repositories {
    jcenter()
  }
  dependencies {
    classpath 'com.neenbedankt.gradle.plugins:android-apt:1.4'
  }
}
 
android {
  ...
}
 
dependencies {
  apt 'com.google.dagger:dagger-compiler:2.0'
  compile 'com.google.dagger:dagger:2.0'
  
  ...
}
```

As you can see we are adding the compiler, the runtime library and the apt plugin, which is necessary, otherwise the dagger annotation processor might not work properly, especially I encountered problems on Android Studio.

������ʾ����������˱�������п⣬���бز����ٵ�apt�����û��������dagger���ܲ��������������ر�����Android studio�С�

Our example
A few months ago I wrote an article about how to implement uncle bob��s clean architecture on Android, which I strongly recommend to read so you get a better understanding of what we are gonna do here. Back then, I faced a problem when constructing and providing dependencies of most of the objects involved in my solution, which looked something like this (check out the comments):
#����
������ǰ����д��һƪ���������Android��ʵ��bob����������ܹ������£�ǿ�ҽ�����ȥ��һ�£�����֮���㽫��������������������и��õ���⡣�Թ�������������ǰ�ķ����У�������ṩ����������������ʱ�򣬻��������⣬�������£�����ע����
```java
  @Override void initializePresenter() {
    // All this dependency initialization could have been avoided by using a
    // dependency injection framework. But in this case this is used this way for
    // LEARNING EXAMPLE PURPOSE.
    ThreadExecutor threadExecutor = JobExecutor.getInstance();
    PostExecutionThread postExecutionThread = UIThread.getInstance();

    JsonSerializer userCacheSerializer = new JsonSerializer();
    UserCache userCache = UserCacheImpl.getInstance(getActivity(), userCacheSerializer,
        FileManager.getInstance(), threadExecutor);
    UserDataStoreFactory userDataStoreFactory =
        new UserDataStoreFactory(this.getContext(), userCache);
    UserEntityDataMapper userEntityDataMapper = new UserEntityDataMapper();
    UserRepository userRepository = UserDataRepository.getInstance(userDataStoreFactory,
        userEntityDataMapper);

    GetUserDetailsUseCase getUserDetailsUseCase = new GetUserDetailsUseCaseImpl(userRepository,
        threadExecutor, postExecutionThread);
    UserModelDataMapper userModelDataMapper = new UserModelDataMapper();

    this.userDetailsPresenter =
        new UserDetailsPresenter(this, getUserDetailsUseCase, userModelDataMapper);
  }
```

As you can see, the way to address this problem is to use a dependency injection framework. We basically get rid of that boilerplate code (which is unreadable and understandable): this class must not know anything about object creation and dependency provision.

So how do we do it? Of course we use Dagger 2 features�� Let me picture the structure of my dependency injection graph:

���Կ���������������İ취��ʹ������ע���ܡ�����Ҫ�����������������ô��룺����಻���漰����Ĵ������������ṩ��
�����Ǹ���ô���أ���Ȼ��ʹ��Dagger2�������ȿ����ṹͼ��
![pic2](http://fernandocejas.com/wp-content/uploads/2015/04/composed_dagger_graph1.png)

Let��s break down this graphic and explain its parts plus some code.

Application Component: A component whose lifetime is the life of the application. It injects both AndroidApplication and BaseActivity classes.

���������ǻ�ֽ�����ͼ�������͸������ֻ��д��롣
Application Component: �������ڸ�Applicationһ�����������ע�뵽AndroidApplication��BaseActivity�����С�

```java
@Singleton // Constraints this component to one-per-application or unscoped bindings.
@Component(modules = ApplicationModule.class)
public interface ApplicationComponent {
  void inject(BaseActivity baseActivity);

  //Exposed to sub-graphs.
  Context context();
  ThreadExecutor threadExecutor();
  PostExecutionThread postExecutionThread();
  UserRepository userRepository();
}
```
As you can see, I use the @Singleton annotation for this component which constraints it to one-per-application. You might be wondering why I��m exposing the Context and the rest of the classes. This is actually an important property of how components work in Dagger: they do not expose types from their modules unless you explicitly make them available. In this case in particular I just exposed those elements to subgraphs and if you try to remove any of them, a compilation error will be triggered.

��Ϊ������ʹ����@Singletonע�⣬ʹ�䱣֤Ψһ�ԡ�Ҳ�������Ϊʲô��Ҫ��context��������Ա��¶��ȥ��������Dagger��components��������Ҫ���ʣ�����㲻���modules�����ͱ�¶��������ô���ֻ����ʾ��ʹ�����ǡ�����������У��Ұ���ЩԪ�ر�¶����ͼ������������ɾ���������ʱ��ͻᱨ��

Application Module: This module provides objects which will live during the application lifecycle, that is the reason why all of @Provide methods use a @Singleton scope.

Application Module: module���������ṩ��Ӧ�õ����������д��Ķ�����Ҳ��Ϊʲô@Provideע��ķ���Ҫ��@Singleton�޶���

```java
@Module
public class ApplicationModule {
  private final AndroidApplication application;

  public ApplicationModule(AndroidApplication application) {
    this.application = application;
  }

  @Provides @Singleton Context provideApplicationContext() {
    return this.application;
  }

  @Provides @Singleton Navigator provideNavigator() {
    return new Navigator();
  }

  @Provides @Singleton ThreadExecutor provideThreadExecutor(JobExecutor jobExecutor) {
    return jobExecutor;
  }

  @Provides @Singleton PostExecutionThread providePostExecutionThread(UIThread uiThread) {
    return uiThread;
  }

  @Provides @Singleton UserCache provideUserCache(UserCacheImpl userCache) {
    return userCache;
  }

  @Provides @Singleton UserRepository provideUserRepository(UserDataRepository userDataRepository) {
    return userDataRepository;
  }
}
```

Activity Component: A component which will live during the lifetime of an activity.

Activity Component: �������ڸ�Activityһ���������

```java
@PerActivity
@Component(dependencies = ApplicationComponent.class, modules = ActivityModule.class)
public interface ActivityComponent {
  //Exposed to sub-graphs.
  Activity activity();
}
```

The @PerActivity is a custom scoping annotation to permit objects whose lifetime should conform to the life of the activity to be memorized in the correct component. I really encourage to do this as a good practice, since we get these advantages:

The ability to inject objects where and activity is required to be constructed.
The use of singletons on a per-activity basis.
The global object graph is kept clear of things that can be used only in activities.

@PerActivity��һ���Զ���ķ�Χע�⣬������������󱻼�¼����ȷ������У���Ȼ��Щ�������������Ӧ����ѭactivity���������ڡ�����һ���ܺõ���ϰ���ҽ������Ƕ���һ�£������ºô���

* ע����󵽹��췽����Ҫ��activity��
* ��һ��per-activity�����ϵĵ���ʹ�á�
* ֻ����activity��ʹ��ʹ��ȫ�ֵĶ���ͼ����������

���´��룺
```java
@Scope
@Retention(RUNTIME)
public @interface PerActivity {}
```

Activity Module: This module exposes the activity to dependents in the graph. The reason behind this is basically to use the activity context in a fragment for example.

Activity Module: �ڶ���ͼ�У����module��activity��¶����������ࡣ������fragment��ʹ��activity��context��

```java
@Module
public class ActivityModule {
  private final Activity activity;

  public ActivityModule(Activity activity) {
    this.activity = activity;
  }

  @Provides @PerActivity Activity activity() {
    return this.activity;
  }
}
```
User Component: A scoped @PerActivity component that extends ActiviyComponent. Basically I use it in order to injects user specific fragments. Since ActivityModule exposes the activity to the graph (as mentioned earlier), whenever an activity context is needed to satisfy a dependency, Dagger will get it from there and inject it: there is no need to re define it in sub modules.

User Component: �̳���ActivityComponent�����������@PerActivityע�⡣��ͨ������ע���û���ص�fragment��ʹ�á���ΪActivityModule��activity��¶��ͼ�ˣ��������κ���Ҫһ��activity��context��ʱ��Dagger�������ṩע�룬û��Ҫ������modules�ж����ˡ�

```java
@PerActivity
@Component(dependencies = ApplicationComponent.class, modules = {ActivityModule.class, UserModule.class})
public interface UserComponent extends ActivityComponent {
  void inject(UserListFragment userListFragment);
  void inject(UserDetailsFragment userDetailsFragment);
}
```

User Module: A module that provides user related collaborators. Based on the example, it will provide user use cases basically.

User Module: �ṩ���û���ص�ʵ�����������ǵ����ӣ��������ṩ�û�������

```java
@Module
public class UserModule {
  @Provides @PerActivity GetUserListUseCase provideGetUserListUseCase(GetUserListUseCaseImpl getUserListUseCase) {
    return getUserListUseCase;
  }

  @Provides @PerActivity GetUserDetailsUseCase provideGetUserDetailsUseCase(GetUserDetailsUseCaseImpl getUserDetailsUseCase) {
    return getUserDetailsUseCase;
  }
}
```

Putting everything together
Now we have our dependency injection graph implementation, how do we inject dependencies? Something we need to know is that Dagger give us a bunch of options to inject dependencies:

Constructor injection: by annotating the constructor of our class with @Inject.
Field injection: by annotating a (non private) field of our class with @Inject.
Method injection: by annotating a method with @Inject.
#���ϵ�һ��
���������Ѿ�ʵ��������ע��ͼ�������Ҹ����ע�룿������Ҫ֪����Dagger��������һ��ѡ������ע��������

 1. ���췽��ע�룺����Ĺ��췽��ǰ��ע��@Inject
 2. ��Ա����ע�룺����ĳ�Ա��������˽�У�ǰ��ע��@Inject
 3. ��������ע�룺�ں���ǰ��ע��@Inject

This is also the order used by Dagger when binding dependencies and it is important because it might happen that you have some strange behavior or even NullPointerExceptions, which means that your dependencies might not have been initialized at the moment of the object creation. This is common on Android when using field injection in Activities or Fragments, since we do not have access to their constructors.

���˳����Dagger����ʹ�õģ���Ϊ�����еĹ����У��ܻ���һЩ��ֵ����������ǿ�ָ�룬��Ҳ��ζ����������ڶ��󴴽���ʱ����ܻ�û�г�ʼ����ɡ�����Android��activity����fragment��ʹ�ó�Ա����ע��ᾭ����������Ϊ����û�������ǵĹ��췽����ʹ�á�

Getting back to our example, let��s see how we can inject a member to our BaseActivity. In this case we do it with a class called Navigator which is responsible for managing the navigation flow in our app:

�ص����ǵ������У���һ�������������BaseActivity��ע��һ����Ա����������������У�����ע����һ����Navigator���࣬��������Ӧ���и�����������ࡣ

```java
public abstract class BaseActivity extends Activity {

  @Inject Navigator navigator;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    this.getApplicationComponent().inject(this);
  }

  protected ApplicationComponent getApplicationComponent() {
    return ((AndroidApplication)getApplication()).getApplicationComponent();
  }

  protected ActivityModule getActivityModule() {
    return new ActivityModule(this);
  }
}
```

Since Navigator is bound by field injection it is mandatory to be provided explicitly in our ApplicationModule using @Provide annotation. Finally we initialize our component and call the inject() method in order to inject our members. We do this in the onCreate() method of our Activity by calling getApplicationComponent(). This method has been added here for reusability and its main purpose is to retrieve the ApplicationComponent which was initialized in the Application object.

Navigator���ǳ�Ա����ע��ģ���ApplicationModule����@Provideע����ʾ�ṩ�ġ��������ǳ�ʼ��componentȻ�����inject()����ע���Ա����������ͨ����Activity��onCreate()�����е���getApplicationComponent()�������Щ������getApplicationComponent()�������������Ϊ�˸����ԣ�������Ҫ������Ϊ�˻�ȡʵ������ApplicationComponent����

Let��s do the same with a presenter in a Fragment. In this case the approach is a bit different since we are using a per-activity scoped component. So our UserComponent which will inject UserDetailsFragment will reside in our UserDetailsActivity:

��Fragment��presenter������Ҳ����ͬ�������飬����Ļ�ȡ������һ�㲻һ������Ϊ������ʹ�õ���per-activity��Χ�޶���component����������ע�뵽UserDetailsFragment�е�UserComponent��ʵ��פ����UserDetailsActivity�еġ�

```java
private UserComponent userComponent;
```
We have to initialize it this way in the onCreate() method of the activity:
���Ǳ�����activity��onCreate()������������ķ�ʽ��ʼ����
```java
private void initializeInjector() {
  this.userComponent = DaggerUserComponent.builder()
      .applicationComponent(getApplicationComponent())
      .activityModule(getActivityModule())
      .build();
}
```
As you can see when Dagger processes our annotations, creates implementations of our components and rename them adding a ��Dagger�� prefix. Since this is a composed component, when constructing it, we must pass in all its dependencies (both components and modules). Now that our component is ready, we just make it accesible in order to satisfy the fragment dependencies:

Dagger�ᴦ�����ǵ�ע�⣬Ϊcomponents����ʵ�ֲ����������ϡ�Dagger��ǰ׺����Ϊ�����һ����ϵ�component�������ڹ�����ʱ�����Ǳ�������е������Ĵ���ȥ��components��modules�����������ǵ�component�Ѿ�׼�����ˣ�����Ϊ�˿�������fragment��������������дһ����ȡ������

```java
@Override public UserComponent getComponent() {
  return userComponent;
}
```
We bind UserDetailsFragment dependencies by getting the created component and calling the inject() method passing the Fragment as a parameter:

�������ڿ�������get������ȡ������component��Ȼ�����inject()������Fragment��Ϊ��������ȥ������������˰�UserDetailsFragment������

```java
@Override public void onActivityCreated(Bundle savedInstanceState) {
  super.onActivityCreated(savedInstanceState);
  this.getComponent.inject(this);
}
```

For the complete example, check the repository on github. There is also some refactor happening and I can tell you that one of the main ideas (taken from the official examples) is to have an interface as a contract which will be implemented by every class that has a component. Something like this:

[��Ҫ�鿴���������ӣ�����ȥ�ҵ�github](https://github.com/android10/Android-CleanArchitecture).��������һЩ�ط��ع��˵ģ��ҿ��Ը�����һ����Ҫ��˼�루���Թٷ������ӣ��ǣ�

```java
public interface HasComponent<C> {
  C getComponent();
}
```

Thus, the client (for example a Fragment) can get the component (from the Activity) and use it:
��ˣ��ͻ��ˣ�����fragment�����Ի�ȡ����ʹ��component������activity����
```java
@SuppressWarnings("unchecked")
protected <C> C getComponent(Class<C> componentType) {
  return componentType.cast(((HasComponent<C>)getActivity()).getComponent());
}
```
The use of generics here makes mandatory to do the casting but at least is gonna fail fast whether the client cannot get a component to use. Just ping me if you have any thoughts/ideas on how to solve this in a better way.
���ʹ����ǿ��ת������������ͻ��˲��ܻ�ȡ�����õ�component���������ٺܿ�ͻ�ʧ�ܡ���������κ��뷨�ܹ����õؽ��������⣬������ҡ�

Dagger 2 code generation
After having a taste of Dagger��s main features, let��s see how does its job under the hood. To illustrate this, we are gonna take again the Navigator class and see how it is created and injected.
First let��s have a look at our DaggerApplicationComponent which is an implementation of our ApplicationComponent:
#Dagger2���ɵĴ���
���˽�Dagger����Ҫ����֮���������������ڲ����졣Ϊ�˾���˵�������ǻ�����Navigator�࣬����������δ�����ע��ġ��������ǿ�һ�����ǵ�DaggerApplicationComponent��
```java
@Generated("dagger.internal.codegen.ComponentProcessor")
public final class DaggerApplicationComponent implements ApplicationComponent {
  private Provider<Navigator> provideNavigatorProvider;
  private MembersInjector<BaseActivity> baseActivityMembersInjector;

  private DaggerApplicationComponent(Builder builder) {  
    assert builder != null;
    initialize(builder);
  }

  public static Builder builder() {  
    return new Builder();
  }

  private void initialize(final Builder builder) {  
    this.provideNavigatorProvider = ScopedProvider.create(ApplicationModule_ProvideNavigatorFactory.create(builder.applicationModule));
    this.baseActivityMembersInjector = BaseActivity_MembersInjector.create((MembersInjector) MembersInjectors.noOp(), provideNavigatorProvider);
  }

  @Override
  public void inject(BaseActivity baseActivity) {  
    baseActivityMembersInjector.injectMembers(baseActivity);
  }

  public static final class Builder {
    private ApplicationModule applicationModule;
  
    private Builder() {  
    }
  
    public ApplicationComponent build() {  
      if (applicationModule == null) {
        throw new IllegalStateException("applicationModule must be set");
      }
      return new DaggerApplicationComponent(this);
    }
  
    public Builder applicationModule(ApplicationModule applicationModule) {  
      if (applicationModule == null) {
        throw new NullPointerException("applicationModule");
      }
      this.applicationModule = applicationModule;
      return this;
    }
  }
}
```
Two important things: the first one is that since we are gonna inject our activity, we have a members injector (which Dagger translates to BaseActivity_MembersInjector):
�������ص���Ҫע�⡣��һ������������Ҫ������ע�뵽activity�У����Ի�õ�һ��ע������ȳ�Ա��ע��������Dagger���ɵ�BaseActivity_MembersInjector����
```java
@Generated("dagger.internal.codegen.ComponentProcessor")
public final class BaseActivity_MembersInjector implements MembersInjector<BaseActivity> {
  private final MembersInjector<Activity> supertypeInjector;
  private final Provider<Navigator> navigatorProvider;

  public BaseActivity_MembersInjector(MembersInjector<Activity> supertypeInjector, Provider<Navigator> navigatorProvider) {  
    assert supertypeInjector != null;
    this.supertypeInjector = supertypeInjector;
    assert navigatorProvider != null;
    this.navigatorProvider = navigatorProvider;
  }

  @Override
  public void injectMembers(BaseActivity instance) {  
    if (instance == null) {
      throw new NullPointerException("Cannot inject members into a null reference");
    }
    supertypeInjector.injectMembers(instance);
    instance.navigator = navigatorProvider.get();
  }

  public static MembersInjector<BaseActivity> create(MembersInjector<Activity> supertypeInjector, Provider<Navigator> navigatorProvider) {  
      return new BaseActivity_MembersInjector(supertypeInjector, navigatorProvider);
  }
}
```
Basically, this guy contains providers for all the injectable members of our Activity so when we call inject() will take the accessible fields and bind the dependencies.
���ע����һ�㶼��Ϊ����activity��ע���Ա�ṩ������ֻҪ����һ����inject()�������Ϳ��Ի�ȡ��Ҫ���ֶκ�������

The second thing, regarding our DaggerApplicationComponent, is that we have a Provider<Navigator> which is no more than interface which provides instances of our class and it is constructed by a ScopedProvider (in the initialize() method) which will memorize the scope of the created class.

�ڶ����ص㣺�������ǵ�DaggerApplicationComponent�࣬������һ��Provider������������һ���ṩʵ���Ľӿڣ������Ǳ�ScopedProvider��������ģ����Լ�¼����ʵ���ķ�Χ��

Dagger also generated a Factory called ApplicationModule_ProvideNavigatorFactory for our Navigator which is passed as a parameter to the mentioned ScopedProvider in order to get scoped instances of our class.
Dagger����Ϊ���ǵ�Navigator������һ������ApplicationModule_ProvideNavigatorFactory�Ĺ���������������Դ��������ᵽ�ķ�Χ����Ȼ��õ������Χ�ڵ����ʵ����

```java
@Generated("dagger.internal.codegen.ComponentProcessor")
public final class ApplicationModule_ProvideNavigatorFactory implements Factory<Navigator> {
  private final ApplicationModule module;

  public ApplicationModule_ProvideNavigatorFactory(ApplicationModule module) {  
    assert module != null;
    this.module = module;
  }

  @Override
  public Navigator get() {  
    Navigator provided = module.provideNavigator();
    if (provided == null) {
      throw new NullPointerException("Cannot return null from a non-@Nullable @Provides method");
    }
    return provided;
  }

  public static Factory<Navigator> create(ApplicationModule module) {  
    return new ApplicationModule_ProvideNavigatorFactory(module);
  }
}
```
This class is actually very simple, it delegates to our ApplicationModule (which contains our @Provide method()) the creation of our Navigator class.

In conclusion, this really looks like hand-written code and it is very easy to understand which makes it easy to debug. There is still much to explore here and a good idea is start debugging and see how Dagger deal with dependency binding.

�����ǳ��򵥣����������ǵ�ApplicationModule������@Provide������������Navigator�ࡣ
��֮������Ĵ��뿴�������������ó����ģ����ҷǳ�����⣬���ڵ��ԡ����໹�кܶ����ȥ̽�������ǿ���ͨ������ȥ����Dagger�����������󶨵ġ�
![pic3](http://fernandocejas.com/wp-content/uploads/2015/04/debugging_dagger.png)

#Դ��:
����: https://github.com/android10/Android-CleanArchitecture
#�������:
[Architecting Android��The clean way?](http://fernandocejas.com/2014/09/03/architecting-android-the-clean-way/)
[Dagger 2, A New Type of Dependency Injection.](https://www.youtube.com/watch?v=oK_XtfXPkqw)
[Dependency Injection with Dagger 2.](https://speakerdeck.com/jakewharton/dependency-injection-with-dagger-2-devoxx-2014)
[Dagger 2 has Components.](https://publicobject.com/2014/11/15/dagger-2-has-components/)
[Dagger 2 Official Documentation.](http://google.github.io/dagger/)