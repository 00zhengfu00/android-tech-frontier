��ӭ�������߳�ʱ��
---

>
* ���� : [Lollypo](https://github.com/Lollypo) 
* У����: [Mr.Simple](https://github.com/bboyfeiyu)  
* ״̬ :  δ���


###That moment when one Dalvik alone is no longer enough.


�������ڴ�������
---

�кܶ෽��ʹ��Android��Ϊһ�����ص��ƶ�����ϵͳ,����ʱ�Ƿǳ����ԽӴ�,�ر��Ǵӿ�����Ա�Ƕ�������

����,���ڴ����ơ�iOSӦ�ó����ṩ����û�����Ƶ��ڴ�Ԥ��(200 MB����ʲô���˵���),Android�����صľ�����,������豸��24/32/48 MB�Լ����豸��С��16 MB����Կ�����

RAMԤ�����һ�����Ӧ�ù���ʱ���ܻ�õ�ȫ���ˣ�����ζ�ţ���������������ࡢ�̡߳�������Դ�����Ӧ�ó�����Ҫ��ʾ�����ݡ�����һ��ͨ��������ͼչʾ����ͼƬ����Ƭ���Ӧ��,��һ����Ҫ�ں�̨���ŵ����ֲ�����:��̫�ֲ���

> ��ʱ��������Ӧ����������

![Life��s a bitch, sometimes.](https://raw.githubusercontent.com/Lollypo/android-tech-frontier/master/others/%E6%AC%A2%E8%BF%8E%E6%9D%A5%E5%88%B0%E5%A4%9A%E7%BA%BF%E7%A8%8B%E6%97%B6%E4%BB%A3/images/img01.gif)

Ҫ���ΪʲôAndroid�������Щ�����Լ��ṩ��ʲô���������Ӧ������,������Ҫ֪��һ������ⱳ��֮������Щʲô��

���Android����
---

ʹ�ö������ɶ�ô�
---

ʹ�ö����ʱ����Щ��  
---

����Ҫʹ�ö������
---

��Ȼ,��ȡ��������Ҫ�鿴���ļ����������û����ھ���Խ��ԽƵ��OutOfMemory����������Ǳ�Թ���Ӧ�ó����Ǽ�������RAM,�������Ҫ����ʹ��һ�����������Ľ��̡�

���ֲ������������ǵڶ���������ʹ���App���ĸ��õ����������һ����������Ȼ�����и��ࡣ
����,���Ӧ�ó�����һ���ͻ����ƴ洢����ί��ͬ���������ר�õĽ����ƺ�����ȫ����ģ����Լ�ʹUI�ᱻϵͳɱ����������Ȼ�������в��ұ����ļ����¡�

> ���Ƶ�����ᷢ�������һ��������ʶ�����̸������˼ʱ

![This happens when you first realize what ��isolation between processes�� really means.](https://raw.githubusercontent.com/Lollypo/android-tech-frontier/master/others/%E6%AC%A2%E8%BF%8E%E6%9D%A5%E5%88%B0%E5%A4%9A%E7%BA%BF%E7%A8%8B%E6%97%B6%E4%BB%A3/images/img04.gif)

�������Ϊ����Ҫ��,��ô�ҽ���������һ��С����̨Ӧ��:ֻ��ͨ��ʵ������ʹ�ö�����̵����ƺ����ڵĸ����ԣ�����ܹ��������Ƿ������Ҫ��,���������,ʲô����õĴ������ķ�ʽ�������ڰ����ǱƷ衣

����
---

��֪���ҽ����������������ı��棬��ֻ�������һЩʵ�õĽ��飬�����Ǹ������ڲ���ϵͳ����ؽ��̵�ȫ�������빤�����ơ�

�����Ǿ仰�������Դ˸���Ȥ��Ը���������У��Ǿ���������֪����ͬʱ����Ҫ�����ĵ�������õ�����[[1]](http://developer.android.com/guide/components/processes-and-threads.html#Processes) [[2]](https://developer.android.com/training/articles/memory.html) [[3]](https://developer.android.com/tools/debugging/debugging-memory.html)

## ԭ������
[Going multiprocess on Android](https://medium.com/@rotxed/going-multiprocess-on-android-52975ed8863c)