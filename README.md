SeimiCrawler
==========
An agile,powerful,standalone,distributed crawler framework.

SeimiCrawler��Ŀ���ǳ�ΪJava������ʵ�õ������ܣ���ӭ���һ��Ŭ����

# ��� #

SeimiCrawler��һ�����ݵģ���������ģ�֧�ֲַ�ʽ��Java�����ܣ�ϣ���������̶��Ͻ������ֿ���һ�������Ը������ܲ��������ϵͳ���ż����Լ�������������ϵͳ�Ŀ���Ч�ʡ���SeimiCrawler����������������ֻ�����ȥдץȡ��ҵ���߼��͹��ˣ������Seimi����㶨�����˼����SeimiCrawler��Python��������Scrapy�����ܴ�ͬʱ�ں���Java���Ա����ص���Spring�����ԣ���ϣ���ڹ��ڸ��������ձ��ʹ�ø���Ч�ʵ�XPath����HTML������SeimiCrawlerĬ�ϵ�HTML��������[JsoupXpath](http://jsoupxpath.wanghaomiao.cn)(������չ��Ŀ����jsoup�Դ�),Ĭ�Ͻ�����ȡHTML���ݹ�����ʹ��XPath����ɣ���Ȼ�����ݴ������������ѡ����������������

# �������� #
�����ʲô����������ڶ�����ѡ��ͨ��������ʼ��б����ۣ��״η���ǰ���ȶ��Ĳ��ȴ����ͨ������Ҫ�������ι�������ȣ�
- ����:�뷢�ʼ��� `seimicrawler+subscribe@googlegroups.com`
- ����:�뷢�ʼ��� `seimicrawler@googlegroups.com`
- �˶�:�뷢�ʼ��� `seimicrawler+unsubscribe@googlegroups.com`

# ���� #
2016.01.05��ר��ΪSeimiCrawler���̴�������`maven-seimicrawler-plugin`�Ѿ��������ã���ϸ���������[maven-seimicrawler-plugin](https://github.com/zhegexiaohuozi/maven-seimicrawler-plugin)��������`���̻��������`�½ڡ�

# ԭ��ʾ�� #
## ����ԭ�� ##
![SeimiCrawlerԭ��ͼ](http://77g8ty.com1.z0.glb.clouddn.com/v2_Seimi.png)

## ��Ⱥԭ�� ##
![SeimiCrawler��Ⱥԭ��ͼ](http://77g8ty.com1.z0.glb.clouddn.com/v1_distributed.png)

# ���ٿ�ʼ #

���maven����(����maven�����°汾0.2.7)��
```
<dependency>
    <groupId>cn.wanghaomiao</groupId>
    <artifactId>SeimiCrawler</artifactId>
    <version>0.2.7</version>
</dependency>
```

�ڰ�`crawlers`���������������磺
```
@Crawler(name = "basic")
public class Basic extends BaseSeimiCrawler {
    @Override
    public String[] startUrls() {
        return new String[]{"http://www.cnblogs.com/"};
    }
    @Override
    public void start(Response response) {
        JXDocument doc = response.document();
        try {
            List<Object> urls = doc.sel("//a[@class='titlelnk']/@href");
            logger.info("{}", urls.size());
            for (Object s:urls){
                push(new Request(s.toString(),"getTitle"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    public void getTitle(Response response){
        JXDocument doc = response.document();
        try {
            logger.info("url:{} {}", response.getUrl(), doc.sel("//h1[@class='postTitle']/a/text()|//a[@id='cb_post_title_url']/text()"));
            //do something
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
Ȼ�����ĳ�������������Main����������SeimiCrawler��
```
public class Boot {
    public static void main(String[] args){
        Seimi s = new Seimi();
        s.start("basic");
    }
}
```
���ϱ���һ����򵥵�����ϵͳ�������̡�

## ���̻�������� ##
������Է���������������ǵ��ԣ���ȻҲ���Գ�Ϊ����������һ��������ʽ�����ǣ�Ϊ�˱��ڹ��̻�������ַ���SeimiCrawler�ṩ��ר�ŵĴ�����������SeimiCrawler���̽��д������õİ�����ֱ�ӷַ����������ˡ�

pom��������plugin
```
<plugin>
    <groupId>cn.wanghaomiao</groupId>
    <artifactId>maven-seimicrawler-plugin</artifactId>
    <version>1.0.0</version>
    <executions>
        <execution>
            <phase>package</phase>
            <goals>
                <goal>build</goal>
            </goals>
        </execution>
    </executions>
    <!--<configuration>-->
        <!-- Ĭ��targetĿ¼ -->
        <!--<outputDirectory>/some/path</outputDirectory>-->
    <!--</configuration>-->
</plugin>
```
ִ��`mvn clean package`���ɣ���ð�Ŀ¼�ṹ���£�
```
.
������ bin             # ��Ӧ�Ľű���Ҳ�о�����������˵�����ܣ��ڴ˲��ٰ���
��   ������ run.bat    #windows�������ű�
��   ������ run.sh     #Linux�������ű�
������ seimi
    ������ classes     #Crawler����ҵ���༰��������ļ�Ŀ¼
    ������ lib         #����������Ŀ¼
```
�������Ϳ���ֱ�������ַ��벿���ˡ�

> ��ϸ���������[maven-seimicrawler-plugin](https://github.com/zhegexiaohuozi/maven-seimicrawler-plugin)

# �����ĵ� #

Ŀǰ���Բο�demo�����е�������������������Ҫ�������÷�����Ϊϸ�µ��ĵ��Ʋ�[SeimiCrawler��ҳ](http://seimi.wanghaomiao.cn)�н�һ���鿴

# Change log #

## v0.2.7 ##
- ��Ƕhttp�ӿ��ڿ��Խ��յ���Json��ʽRequest����������֧�ֽ���Json������ʽ�Ķ��Request
- `Request`����֧������`skipDuplicateFilter`��������seimi����������ȥ�ػ��ƣ�Ĭ�ϲ�����
- ���Ӷ�ʱ����ʹ��Demo
- �ص�����ͨ��Request�����Զ������ֵ������Object��ΪString��������ȷ����
- Fix:�޸�һ������־��bug

## v0.2.6 ##
- ����ͳһ����������࣬���δ��SeimiCrawler��maven����pluginһ��ʹ��
- meta refresh��ʽ��ת�Ż��������������Ϊ3�Σ���ֹ��������ˢ��ҳ���޷�����
- bug fix:�޸���Request���Զ��������޷�����Response������

## v0.2.5 ##
- �����������������쳣ʱ���´�ض��д������
��һ�������ھ������������쳣�����Ի��ƺ���Ȼ���ַ�Ԥ���쳣����ô���������ڲ��������������õĻ���Ĭ�ϵ�������´������������±���ض������µȴ��������������ش����ﵽ��������ƣ���ôseimi����ÿ��������и���ʵ�ֵ�`BaseSeimiCrawler.handleErrorRequest(Request request)`�������¼����쳣���������´�صȴ�����������delay����ʹ�ÿ����ںܴ�̶��ϱ��������վ��ķ��������������������쳣������ʧ����ļ�¼�������
- �Ż�ȥ���ж�
- �Ż����淶ҳ��ı����ȡ��ʽ

## v0.2.4 ##
- �Զ���ת��ǿ����301,302������֧��ʶ��ͨ��meta refresh��ʽ��ҳ����ת
- `Response`��������ͨ��`getRealUrl()`��ȡ���ݶ�Ӧ�ض����Լ���ת�����ʵ����
- ͨ��ע��@Crawler��'useUnrepeated'���Կ����Ƿ�����ϵͳ��ȥ�ػ��ƣ�Ĭ�Ͽ���

## v0.2.3 ##
- ֧���Զ��嶯̬����
�����߿���ͨ������`BaseSeimiCrawler.proxy()`�����о���ÿ��������ʹ�õĴ������Ǹ÷�����������Ч�����ַ��`@Crawler`��`proxy`����ʧЧ��
- ��Ӷ�̬������̬User-Agentʹ��demo

## v0.2.2 ##
- ��ǿ�Բ��淶��ҳ�ı���ʶ�����������

## v0.2.1 ##
- �Ż��ڰ�����������˻���

## v0.2.0 ##
- ����֧����Ƕhttp����API�ύjson��ʽ��Request����
- �����������URL����У���`allowRules`��`denyRules`���Զ������ã�������������ͺ��������򣬸�ʽ��Ϊ������ʽ��Ĭ��Ϊnull�����м��
- ���Ӷ�Request�ĺϷ��Ե�ͳһУ��
- ����֧��������delayʱ������

# ��ĿԴ�� #
[Github](https://github.com/zhegexiaohuozi/SeimiCrawler)
> **BTW:**
> ��������������Ŀ������github��`star`һ�£����ǲ������ ^_^