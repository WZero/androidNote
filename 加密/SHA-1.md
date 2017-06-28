## SHA-1 ##

- SHA-1（英语：Secure Hash Algorithm 1，中文名：安全散列算法1）是一种密码散列函数，美国国家安全局设计，并由美国国家标准技术研究所（NIST）发布为联邦数据处理标准（FIPS）。SHA-1可以生成一个被称为消息摘要的160位（20字节）散列值，散列值通常的呈现形式为40个十六进制数。   

- SHA-1已经不再视为可抵御有充足资金、充足计算资源的攻击者。2005年，密码分析人员发现了对SHA-1的有效攻击方法，这表明该算法可能不够安全，不能继续使用，自2010年以来，许多组织建议用SHA-2或SHA-3来替换SHA-1。Microsoft、Google以及Mozilla都宣布，它们旗下的浏览器将在2017年前停止接受使用SHA-1算法签名的SSL证书。   

- 2017年2月23日，CWI Amsterdam（英语：CWI Amsterdam）与Google宣布了一个成功的SHA-1碰撞攻击（英语：Collision_attack），发布了两份内容不同但SHA-1散列值相同的PDF文件作为概念证明。

#### MD5 与SHA-1 的比较 

- 由于MD5 与SHA-1均是从MD4 发展而来，它们的结构和强度等特性有很多相似之处。

- SHA-1与MD5 的最大区别在于其摘要比MD5 摘要长 32 比特。对于强行攻击，产生任何一个报文使之摘要等于给定报文摘要的难度：MD5 是2128 数量级的操作，SHA-1 是2160 数量级的操作。

- 产生具有相同摘要的两个报文的难度：MD5是 264 是数量级的操作，SHA-1 是280 数量级的操作。因而,SHA-1 对强行攻击的强度更大。

- 但由于SHA-1 的循环步骤比MD5 多（80:64）且要处理的缓存大（160 比特:128 比特），SHA-1 的运行速度比MD5 慢。 

### 上代码 

	// 跟获取MD5的代码特别像 基本没变

	import com.sun.istack.internal.NotNull;
	
	import java.math.BigInteger;
	import java.security.MessageDigest;
	import java.security.NoSuchAlgorithmException;
	
	/**
	 * SHA-1 工具类
	 * Created by Wang on 2017/6/28.
	 */
	public class SHA1Util {
	
	    public static void main(String[] strings) {
	        System.out.println("获取SHA-1 :" + toSHA1String("123ADAaa"));
	    }
	
	    /**
	     * 获取 SHA-1 指纹
	     *
	     * @param string String
	     * @return String
	     */
	    public static String toSHA1String(@NotNull String string) {
	        try {
	            MessageDigest messageDigest = MessageDigest.getInstance("SHA-1");// 创建具有指定算法名称的信息摘要。
	            byte[] digest = messageDigest.digest(string.getBytes());//使用指定的 byte 数组对摘要进行最后更新，然后完成摘要计算。
	            return new BigInteger(1, digest).toString(16);// digest 计算后的byte[] 二进制 转换为16进制
	        } catch (NoSuchAlgorithmException e) {
	            e.printStackTrace();
	            return null;
	        }
	    }
	}
	
	//打印结果 
	//获取SHA-1 :4ae53cf936652197ae20a4bcb3d95084949556de


## API ##
#### java.security.MessageDigest 

	MessageDigest.getInstance(String algorithm) 
          	//返回实现指定摘要算法的 MessageDigest 对象。

	MessageDigest.update(byte[] input) 
          	//使用指定的 byte 数组更新摘要。

	MessageDigest.digest(byte[] input) 
	        //使用指定的 byte 数组对摘要进行最后更新，然后完成摘要计算。也就是说，此方法首先调用 update(input)，向 update 方法传递 input 数组，然后调用 digest()。
	
#### java.math.BigInteger   
	BigInteger(int signum, byte[] magnitude) 
	         //将 BigInteger 的符号-数量表示形式转换为 BigInteger。

	BigInteger.toString(int radix) 
          	//返回此 BigInteger 的给定基数的字符串表示形式。

	BigInteger.toString() 
	        //返回此 BigInteger 的十进制字符串表示形式。

#### java.lang.String   

	String.getBytes() 
	        //使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。
	
	String.substring(int beginIndex,int endIndex)
			//返回一个新字符串，它是此字符串的一个子字符串。该子字符串从指定的 beginIndex 处开始，直到索引 endIndex - 1 处的字符
