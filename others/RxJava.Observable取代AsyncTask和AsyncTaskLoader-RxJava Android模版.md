��RxJava.Observableȡ��AsyncTask��AsyncTaskLoader-RxJava Androidģ��
---

>
* ���� : [ZhaoKaiQiang](https://github.com/ZhaoKaiQiang) 
* У����: [chaossss](https://github.com/chaossss)  
* ״̬ :  У���� 


�������кܶ����RxJava����ָ�ϵ����ӣ�����һЩ�ǻ���Android�����ġ����ǣ����뵽ĿǰΪֹ���ܶ���ֻ��ϲ����������������Щ����Ҫ��������ǵ�Android��Ŀ�г��ֵľ�������ʱ�����ǲ���֪����λ�����ΪʲôҪʹ��RxJava������һϵ�е������У�����Ҫ̽�����ҹ�������һЩ������RxJava�ܹ���Android��Ŀ�е�ģʽ��

�����µĿ�ʼ������Ҫ����һЩAndroid��������ʹ��RxJava��ʱ�򣬺�����������״����������Ƕȣ��ҽ��ṩ���߼��͸����ʵĽ������������һϵ�е������У���ϣ����������������������ʹ��RxJava�Ĺ����н�����Ƶ����⣬�������Ǻ��ҷ��ֵ�һ���ء�

#����һ����̨����
Android������������������ս���������Ч���ں�̨�߳��й�����Ȼ����UI�߳��и���UI���⾭������Ϊ��Ҫ��web service�л�ȡ���ݡ������Ѿ�����ؾ��������ܻ�˵��������ʲô��ս�ԣ���ֻ��Ҫ����һ��AsyncTask��Ȼ�����еĹ������Ͷ��������ˡ����������������ģ���ô����һ������ȥ��������״����������Ϊ���Ѿ�ϰ�������ָ��ӵķ�ʽ���������ⱾӦ���Ǻܼ��ģ�������˵��û�д�������Ӧ�ô���ı߽��������������̸̸�����

##Ĭ�ϵĽ��������AsyncTask
AsyncTask����Android����Ĭ�ϵĴ����ߣ������߿���������һЩ��ʱ��Ĵ������������������û����档(ע�⣺�����AsyncTaskLoader��������һЩ���Ӿ�������ݼ������������Ժ����̸̸���)

�����ϣ����ƺ��ܼ򵥣��㶨��һЩ�����ں�̨�߳������У�Ȼ����һЩ����������UI�߳��У��ں�̨��������֮������UI�̻߳ᴦ��Ӻ�̨���񴫵ݹ�����ִ�н����

	private class CallWebServiceTask extends AsyncTask<String, Result, Void> {
    
	    protected Result doInBackground(String... someData) {
	        Result result = webService.doSomething(someData);
	        return result;
	    }
    
	    protected void onPostExecute(Result result) {
	        if (result.isSuccess() {
	            resultText.setText("It worked!");
	        }
	    }
	}

ʹ��AsyncTask��������������ϸ�ڵĴ����ϣ�������̸̸������⡣

###������
���ּ��÷��ĵ�һ��������ǣ�����������˴�����ô�죿�����ҵ��ǣ���ʱû�зǳ��õĽ�����������Ժܶ�Ŀ���������Ҫ�̳�AsyncTask��Ȼ����doInBackground()�а���һ��try/catch������һ��<TResult, Exception>��Ȼ����ݷ�����������ַ����¶��������onSuccess()������onError()�С�(��Ҳ���������������쳣�����ã�Ȼ���� onPostExcecute()�н��м���д��) 

���������е�����ģ����������Ϊ���ÿ����Ŀд�϶���Ĵ��룬����ʱ������ƣ���Щ�Զ���Ĵ����ڿ�����֮�����Ŀ֮�䣬���ܲ��ᱣ�ֺܺõ�һ���ԺͿ�Ԥ���ԡ�

###Activity��Fragment����������
����һ���������Ե������ǣ�����AsyncTask�������е�ʱ��������˳�Activity��������ת�豸�Ļ��ᷢ��ʲô�����ţ������ֻ�Ƿ���һЩ���ݣ�֮��Ͳ��ٹ��ķ��ͽ�����ǿ�����û������ģ������������Ҫ����Task�ķ��ؽ������UI�أ�����㲻��һЩ������ֹ�Ļ�����ô������ͼȥ����Activity������view�Ļ����㽫�õ�һ����ָ���쳣���³����������Ϊ���������ǲ��ɼ�������null�ġ�

ͬ���������������AsyncTaskû�����ܶ๤��ȥ�����㡣��Ϊһ�������ߣ�����Ҫȷ������һ��Task�����ã�����Ҫô��Activity���ڱ����ٵ�ʱ��ȡ��Task��Ҫô������ͼ��onPostExecute()�������UI��ʱ��ȷ��Activity����һ���ɴ�״̬������ֻ����ȷ����һЩ��������������Ŀ����ά����ʱ���⽫��������ά����Ŀ���Ѷȡ�

###��תʱ�Ļ���(�����������)
������û����Ǵ��ڵ�ǰActivity����������ת��Ļ�ᷢ��ʲô������������£�ȡ��Taskû���κ����壬��Ϊ����ת֮�������ջ�����Ҫ��������Task���������㲻������Task����Ϊ״����һЩ�ط��Է�Ļ�ȵķ�ʽ������ͻ��(because it mutates some state somewhere in a non-idempotent way),������ȷʵ��Ҫ�õ��������Ϊ������Ϳ��Ը���UI����ӳ���������

�����ר�ŵ���һ��ֻ���ļ��ز����������ʹ��AsyncTaskLoaderȥ���������⡣���Ƕ��ڱ�׼��Android��ʽ��˵�������Ǻܳ��أ���Ϊȱ�ٴ�������Activity��û�л��棬���кܶ���е�������񱡣

###��ϵĶ��Web Server����
���ڣ�����˵�����Ѿ���취����������ⶼ����ˣ���������������Ҫ��һЩ��������������ÿһ��������Ҫ����ǰһ������Ľ���������ǣ���������һЩ��������������Ȼ��ѽ���ϲ���һ���͵�UI�̣߳����ǣ��ٴα�Ǹ��AsyncTask������ﲻ���㡣

һ���㿪ʼ�����������飬���Ÿ���ĸ����߳�ģ�͵�������֮ǰ������ᵼ�´�������������ǳ���ʹ��Ͳ԰������������Ҫ��Щ�߳�һ�����У�Ҫ����������ǵ������У�Ȼ��ص�����������������£���������һ����̨�߳���ͬ�����У��������ɲ�ͬ��(To chain calls together, you either keep them separate and end up in callback hell, or run them synchronously together in one background task end up duplicating work to compose them differently in other situations.)

���Ҫ�������У�����봴��һ���Զ����executorȻ�󴫵ݸ�AsyncTaskTask����ΪĬ�ϵ�AsyncTask��֧�ֲ��С�����Ϊ��Э�������̣߳�����Ҫʹ������CountDownLatchs, Threads, Executors �� Futuresȥ���͸����ӵ�ͬ��ģʽ��

###�ɲ�����
�׿���Щ��˵�������ϲ��������Ĵ��룬AsyncTask�����ܸ������ʲô������������ǲ�������Ĺ���������AsyncTask�ǳ����ѣ����ܴ�����������ά�֡�����һƪ�й���γɹ�����AsyncTask��[����](http://www.making-software.com/2012/10/31/testable-android-asynctask/)��

##���õĽ��������RxJava��s Observable

���˵��ǣ�һ�����Ǿ���ʹ��RxJava�������ʱ���������۵���Щ����Ͷ�ӭ�ж����ˡ��������ǿ�������Ϊ������ʲô��

�������ǽ���ʹ��Observablesдһ�������������������AsyncTask��ʽ��(�����ʹ��Retrofit����ô��Ӧ�ú�����ʹ�ã��������֧��Observable ����ֵ��������������һ����̨���̳߳أ����������Ĺ���)

	webService.doSomething(someData)
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(
        result -> resultText.setText("It worked!")),
        e -> handleError(e)
    );
	
###������
����ܻ�ע�⵽��û��������Ĺ����������Ѿ�������AsyncTask���ᴦ��ĳɹ��ʹ�����������������д�˺��ٵĴ��롣�㿴���Ķ���������������ҪObserver ��UI���߳��д���Ľ������������������ǰ��һ��㡣����������sebService�������ں�̨�߳������У���Ҳ����������ͨ��ʹ��.subscribeOn(...) ������(ע�⣺��Щ������ʹ��Java 8��lambda�﷨��ʹ��[Retrolambda](https://github.com/orfjackal/retrolambda)�Ϳ�����Android��Ŀ�н���ʹ���ˣ������ҿ������������Ļر��Ǹ��ڷ��յģ���д��ƪ������ȣ����Ǹ�ϲ�������ǵ���Ŀ��ʹ�á�)

###Activity��Fragment����������
���ڣ�����������������RxAndroid��������ᵽ���������ڵ����⣬���ǲ���Ҫָ��mainThread() scheduler(˳��˵һ�䣬��ֻ��Ҫ����RxAndroid)��������������

	AppObservable.bindFragment(this, webService.doSomething(someData))
    .subscribe(
        result -> resultText.setText("It worked!")),
        e -> handleError(e)
    );
	
��ͨ������������Ӧ�õ�Base Fragment���洴��һ����������������һ�㣬����Բο���ά����һ��[Base RxFragment](https://github.com/rosshambrick/standardlib/blob/master/src/main/java/com/rosshambrick/standardlib/RxFragment.java) ���һЩָ����

	bind(webService.doSomething(someData))
    .subscribe(
        result -> resultText.setText("It worked!")),
        e -> handleError(e)
    );
	
������ǵ�Activity������Fragment�����ǿɴ�״̬����ôAppObservable.bindFragment()�����ڵ������в���һ����Ƭ������ֹonNext()���С������Task��ͼ���е�ʱ��Activity��Fragment�ǲ��ɴ�״̬��subscription ����ȡ�����Ĳ���ֹͣ���У����Բ�����ڿ�ָ��ķ��գ�����Ҳ���������һ����Ҫע����ǣ��������뿪Activity��Fragmentʱ�����ǻ���ʱ���������õ�й¶����ȡ���������е�Observable ����Ϊ��������bind()�����У���Ҳ�����LifeCycleObservable���ƣ���Fragment���ٵ�ʱ���Զ�ȡ�����������ĺô���һ�����ݡ�

���ԣ���������Ҫ���������⣬����������һ������RxJava�������ĵط���

###��ϵĶ��Web Server����
�������Ҳ�����ϸ��˵������Ϊ����һ��[���ӵ�����](http://reactivex.io/documentation/observable.html)������ͨ��ʹ��Observables��������÷ǳ��򵥺��������ķ�ʽ��ɸ��ӵ����顣������һ����ʽWeb Service���õ����ӣ���Щ���������������̳߳������еڶ������е��ã�Ȼ���ڽ�������ظ�Observer֮ǰ�������ݽ��кϲ�������Ϊ�˸��õĲ����������������������һ�������������е�ҵ���߼�����������̶����д�������...

	public Observable<List<CityWeather>> getWeatherForLargeUsCapitals() {
    return cityDirectory.getUsCapitals() 
        .flatMap(cityList -> Observable.from(cityList))
        .filter(city -> city.getPopulation() > 500,000)
        .flatMap(city -> weatherService.getCurrentWeather(city)) //each runs in parallel
        .toSortedList((cw1,cw2) -> cw1.getCityName().compare(cw2.getCityName()));
	}

###��תʱ�Ļ���(�����������)
��Ȼ����һ�����ص����ݣ���ô���ǿ�����Ҫ�����ݽ��л��棬������������ת�豸��ʱ�򣬾Ͳ��ᴥ���ٴε���ȫ��web service���¼���һ��ʵ�ֵķ�ʽ�Ǳ���Fragment�����ұ���һ����Observable �Ļ�������ã���������������

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setRetainInstance(true);
        weatherObservable = weatherManager.getWeatherForLargeUsCapitals().cache();
    }

    public void onViewCreated(...) {
        super.onViewCreated(...)
        bind(weatherObservable).subscribe(this);
    }

����ת֮�󣬶����ߵĻ���ʵ���ͻ����������͵�һ��������ͬ�����󣬷�ֹ��ʵ��Web Service��������

�������Ҫ���⻺���Fragment(�����кܳ��������ȥ������)�����ǿ���ͨ��ʹ��AsyncSubjectʵ�ֻ��档���ۺ�ʱ�����ģ�AsyncSubject �������·���������Ŀ���������ǿ���ʹ��BehaviorSubject�������ֵ����ֵ�ı�����Ӧ�ó���

 WeatherListFragment.java 
	
	public void onViewCreated() {
    super.onViewCreated()
    bind(weatherManager.getWeatherForLargeUsCapitals()).subscribe(this);
	}

 WeatherManager.java

	public Observable<List<CityWeather>> getWeatherForLargeUsCapitals() {
    if (weatherSubject == null) {
        weatherSubject = AsyncSubject.create();

        cityDirectory.getUsCapitals() 
            .flatMap(cityList -> Observable.from(cityList))
            .filter(city -> city.getPopulation() > 500,000)
            .flatMap(city -> weatherService.getCurrentWeather(city))
            .toSortedList((cw1,cw2) -> cw1.getCityName().compare(cw2.getCityName()))
            .subscribe(weatherSubject);
    }
    return weatherSubject;
	}

��Ϊ�����桱����Manager��������ģ���������Fragment/Activity�����ڰ󶨣�������Activity/Fragment�н��������ڡ��������ǿ��ˢ�»��������Ƶķ�ʽ������Fragment����ʵ�������������¼����������������


	public void onCreate() {
    super.onCreate()
    if (savedInstanceState == null) {
        weatherManager.invalidate(); //invalidate cache on fresh start
    }
	}

��������ΰ��֮�����ڣ���������Loaders�����ǿ��Ժ����Ļ��򻺴�ܶ�Activity��Services�еĽ����ֻ��Ҫȥ��oncreate()�е�invalidate()���ã��������Manager���������ʱ�����µ��������ݾͿ����ˡ�������һ��Timer���������û���λ�ı䣬�����������κ�ʱ�̣������û��ϵ�������ڿ��Կ���ʲôʱ�����ȥ���»�������¼��ء����ҵ���Ļ�����Է����ı��ʱ��Fragment�����Manager����֮��Ľӿڲ���Ҫ���иı䡣��ֻ������һ�� List<WeatherData>��Observer��

###�ɲ�����
������������Ҫʵ�ָɾ����򵥵����һ����ս��(�����Ǻ���һ����ʵ���ڲ����ڼ�,���ǿ�����Ҫģ���ʵ�ʵ�Web�����������ܼ򵥣�����ͨ��һ���ӿ�ע�뵽��Щ����������Ѿ��������ı�׼ģʽ�С�)

���˵��ǣ�Observables������һ���򵥵ķ�ʽ����һ���첽�������ͬ������Ҫ���ľ���ʹ��toblocking()���������ǿ�һ���������ӡ�

	List results = getWeatherForLargeUsCapitals().toBlocking().first();
	assertEquals(12, results.size());

��������������û�б�Ҫȥʹ��Futures������CountDownLatchs����һЩ�����Ĳ����������߳�˯�߻����������ǵĲ��Ա�úܸ��ӣ����ǵĲ��������Ǽ򵥡��ɾ�����ά���ġ�

##����
���£����Ѿ�������һ�Լ򵥵���Ŀ����ʾ[AsyncTask���](https://github.com/rosshambrick/AsyncExamples)��[AsyncTaskLoader](https://github.com/rosshambrick/rain-or-shine)���

RxJava����ֵ��ӵ�С�����ʹ��rx.Observable���滻AsyncTask��AsyncTaskLoader��ʵ�ָ���ǿ��������Ĵ��롣ʹ��RxJava Observables�ܿ��֣��������ڴ��ܹ����ָ����Android����Ľ��������


## ԭ������
[Replace AsyncTask and AsyncTaskLoader with rx.Observable �C RxJava Android Patterns](http://stablekernel.com/blog/replace-asynctask-asynctaskloader-rx-observable-rxjava-android-patterns/)