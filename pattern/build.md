为什么要学建造者模式模式
> - 什么是建造者模式
> - 建造者模式使用场景
> - 如何实现一个建造者模式
> - 建造者模式优点和缺点

## 什么是建造者模式

建造者模式（Builder Pattern）

由多个简单对象一步一步构建成为一个复杂对象，属于创建型工厂模式

通过一个builder类来一步步实现搭建复杂对象


## 建造者模式使用场景

**1、需要生成的对象具有复杂的内部结构**

**2、需要生成的对象内部属性本身相互依赖。**


## 如何实现一个建造者模式

/**
 * @author jiangtao
 * @version V1.0
 * @Description：支付统一响应报文 <p>创建日期：2019/6/10 </p>
 * @see
 */
public class PayResponseBody {

    //功能码
    private String funCode;
    
    //流水号
    private String rpid;
    
    //商户id
    private String merId;
    
    //交易金额
    private String amount;
    
    //响应日期
    private String resdate;
    
    //响应时间
    private String restime;
    
    //银行卡号
    private String account;
    
    //银行名称
    private String bankName;
    
    //银行信息
    private String bankInfo;

    public String getFunCode() {
        return funCode;
    }

    public void setFunCode(String funCode) {
        this.funCode = funCode;
    }

    public String getRpid() {
        return rpid;
    }

    public void setRpid(String rpid) {
        this.rpid = rpid;
    }

    public String getMerId() {
        return merId;
    }

    public void setMerId(String merId) {
        this.merId = merId;
    }

    public String getAmount() {
        return amount;
    }

    public void setAmount(String amount) {
        this.amount = amount;
    }

    public String getResdate() {
        return resdate;
    }

    public void setResdate(String resdate) {
        this.resdate = resdate;
    }

    public String getRestime() {
        return restime;
    }

    public void setRestime(String restime) {
        this.restime = restime;
    }

    public String getAccount() {
        return account;
    }

    public void setAccount(String account) {
        this.account = account;
    }

    public String getBankName() {
        return bankName;
    }

    public void setBankName(String bankName) {
        this.bankName = bankName;
    }

    public String getBankInfo() {
        return bankInfo;
    }

    public void setBankInfo(String bankInfo) {
        this.bankInfo = bankInfo;
    }

    @Override
    public String toString() {
        return "PayResponseBody{" +
                "funCode='" + funCode + '\'' +
                ", rpid='" + rpid + '\'' +
                ", merId='" + merId + '\'' +
                ", amount='" + amount + '\'' +
                ", resdate='" + resdate + '\'' +
                ", restime='" + restime + '\'' +
                ", account='" + account + '\'' +
                ", bankName='" + bankName + '\'' +
                ", bankInfo='" + bankInfo + '\'' +
                '}';
    }
}

/**
 * @author jiangtao
 * @version V1.0
 * @Description：抽象响应构建工厂 <p>创建日期：2019/6/10 </p>
 * @see
 */
public abstract class PayResponseHandler {

    public abstract void  funCode(String funCode);
    
    public abstract void  rpid(String rpid);
    
    public abstract void  merId(String merId);
    
    public abstract void  amount(String amount);
    
    public abstract void  resdate(String resdate);
    
    public abstract void  restime(String restime);
    
    public abstract void  account(String account);
    
    public void bankName(String bankName){}
    
    public void bankInfo(String bankInfo){}
    
    //创建响应对象
    public abstract PayResponseBody creat();
}

/**
 * @author jiangtao
 * @version V1.0
 * @Description：微信响应对象 <p>创建日期：2019/6/10 </p>
 * @see
 */
public class BankResponseBody extends PayResponseHandler {

    private PayResponseBody payResponseBody = new PayResponseBody();

    @Override
    public void funCode(String funCode) {
        payResponseBody.setFunCode(funCode);
    }

    @Override
    public void rpid(String rpid) {
        payResponseBody.setRpid(rpid);
    }

    @Override
    public void merId(String merId) {
        payResponseBody.setMerId(merId);
    }

    @Override
    public void amount(String amount) {
        payResponseBody.setAmount(amount);
    }

    @Override
    public void resdate(String resdate) {
        payResponseBody.setResdate(resdate);
    }

    @Override
    public void restime(String restime) {
        payResponseBody.setRestime(restime);
    }

    @Override
    public void account(String account) {
        payResponseBody.setAccount(account);
    }
    
    public  void  bankName(String bankName){
        payResponseBody.setBankName(bankName);
    }

    public  void  bankInfo(String bankInfo){
        payResponseBody.setBankInfo(bankInfo);
    }

    @Override
    public PayResponseBody creat() {
        return payResponseBody;
    }

    @Override
    public String toString() {
        return "payResponseBody=" + payResponseBody ;
    }
}

/**
 * @author jiangtao
 * @version V1.0
 * @Description：微信响应对象 <p>创建日期：2019/6/10 </p>
 * @see
 */
public class WxResponseBody extends PayResponseHandler {

    private PayResponseBody payResponseBody = new PayResponseBody();

    @Override
    public void funCode(String funCode) {
        payResponseBody.setFunCode(funCode);
    }

    @Override
    public void rpid(String rpid) {
        payResponseBody.setRpid(rpid);
    }

    @Override
    public void merId(String merId) {
        payResponseBody.setMerId(merId);
    }

    @Override
    public void amount(String amount) {
        payResponseBody.setAmount(amount);
    }

    @Override
    public void resdate(String resdate) {
        payResponseBody.setResdate(resdate);
    }

    @Override
    public void restime(String restime) {
        payResponseBody.setRestime(restime);
    }

    @Override
    public void account(String account) {
        payResponseBody.setAccount(account);
    }

    @Override
    public PayResponseBody creat() {
        return payResponseBody;
    }

    @Override
    public String toString() {
        return "payResponseBody=" + payResponseBody ;
    }
}


/**
 * @author jiangtao
 * @version V1.0
 * @Description：微信响应对象 <p>创建日期：2019/6/10 </p>
 * @see
 */
public class WxResponseBodyBuilder {

    private PayResponseHandler payResponseHandler;

    public WxResponseBodyBuilder(PayResponseHandler payResponseHandler){
        this.payResponseHandler =  payResponseHandler;
    }

    //执行构造参数
    public PayResponseBody constuct(String account,String amount,String funCode,String merId,String resdate,String restime,String rpid){
        
        payResponseHandler.account(account);
        
        payResponseHandler.amount(amount);
        
        payResponseHandler.funCode(funCode);
        
        payResponseHandler.merId(merId);
        
        payResponseHandler.resdate(resdate);
        
        payResponseHandler.restime(restime);
        
        payResponseHandler.rpid(rpid);
        
        return  payResponseHandler.creat();
    }


}

/**
 * @author jiangtao
 * @version V1.0
 * @Description：微信响应对象 <p>创建日期：2019/6/10 </p>
 * @see
 */
public class BankResponseBodyBuilder{

    private PayResponseHandler payResponseHandler;

    public BankResponseBodyBuilder(PayResponseHandler payResponseHandler){
        this.payResponseHandler =  payResponseHandler;
    }

    //执行构造参数
    public PayResponseBody constuct(String account,String amount,String bankInfo,String bankName,String funCode,String merId,String resdate,String restime,String rpid){
       
        payResponseHandler.account(account);
       
        payResponseHandler.amount(amount);
       
        payResponseHandler.bankInfo(bankInfo);
       
        payResponseHandler.bankName(bankName);
       
        payResponseHandler.funCode(funCode);
       
        payResponseHandler.merId(merId);
       
        payResponseHandler.resdate(resdate);
       
        payResponseHandler.restime(restime);
       
        payResponseHandler.rpid(rpid);
       
        return  payResponseHandler.creat();
    }
    
}

/**
 * @author jiangtao
 * @version V1.0
 * @Description： <p>创建日期：2019/6/11 </p>
 * @see
 */
public class ResponseBuilderTest {
    
    public static void main(String[] args) {
    
        //创建银行卡支付后结果响应报文
        BankResponseBody bankResponseBody = new BankResponseBody();
        
        BankResponseBodyBuilder bankResponseBodyBuilder = new BankResponseBodyBuilder(bankResponseBody);
        
        bankResponseBodyBuilder.constuct("6226090108554561", "1", "招商银行支付", "招商银行", "BankPay", "9996", "20190501", "164004", "123456789");
       
        System.out.println("银行卡响应报文："+bankResponseBody.toString());
        
        //创建微信支付完成后结果响应报文
        WxResponseBody wxResponseBody = new WxResponseBody();
       
        WxResponseBodyBuilder wxResponseBodyBuilder = new WxResponseBodyBuilder(wxResponseBody);
        
        wxResponseBodyBuilder.constuct("123465798555","1","WXpay","9996","20190601","080101","132456789456");
        
        System.out.println("微信响应报文："+wxResponseBody.toString());
    }
}

```
这段代码的输出如下：

银行卡响应报文：

{funCode='BankPay', rpid='123456789', merId='9996', amount='1', resdate='20190501', restime='164004', account='6226090108554561', bankName='招商银行', bankInfo='招商银行支付'}

微信响应报文：

{funCode='WXpay', rpid='132456789456', merId='9996', amount='1', resdate='20190601', restime='080101', account='123465798555', bankName='null', bankInfo='null'}



```

## 建造者模式的优点与缺点
优点
>- 建造者独立，易扩展。
>- 便于控制细节风险。 

缺点
>- 产品必须有共同点，范围有限制
>- 如内部变化复杂，会有很多的建造类