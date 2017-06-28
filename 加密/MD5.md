
## MD5 ##

- MD5消息摘要算法（英语：MD5 Message-Digest Algorithm），一种被广泛使用的密码散列函数，可以产生出一个128位（16字节）的散列值（hash value），用于确保信息传输完整一致。MD5由罗纳德·李维斯特设计，于1992年公开，用以取代MD4算法。这套算法的程序在 RFC 1321 中被加以规范。    

- 将数据（如一段文字）运算变为另一固定长度值，是散列算法的基础原理。   

- 1996年后被证实存在弱点，可以被加以破解，对于需要高度安全性的数据，专家一般建议改用其他算法，如SHA-1。2004年，证实MD5算法无法防止碰撞（collision），因此无法适用于安全性认证，如SSL公开密钥认证或是数字签名等用途。

### 上代码 ##

	import com.sun.istack.internal.NotNull;
	
	import java.math.BigInteger;
	import java.security.MessageDigest;
	import java.security.NoSuchAlgorithmException;
	
	/**
	 * md5 工具类
	 * Created by Wang on 2017/6/28.
	 */
	public class Md5Util {
	    /**
	     * 返回32位的 MD5
	     */
	    public static final int TO_LENGTH_32 = 32;
	    /**
	     * 返回16位的 MD5
	     */
	    public static final int TO_LENGTH_16 = 16;
	
	    public static void main(String[] strings) {
	        System.out.println("32位 MD5 : "+toMd5String("123"));
	        System.out.println("16位 MD5 : "+toMd5String("123", TO_LENGTH_16));
	        System.out.println("32位 MD5 : "+toMd5String("123", TO_LENGTH_32));
	    }

	    /**
	     * 获取32位MD5指纹
	     *
	     * @param string String
	     * @return String
	     */
	    public static String toMd5String(@NotNull String string) {
	        return toMd5String(string, TO_LENGTH_32);
	    }

	    /**
	     * 获取MD5指纹
	     *
	     * @param string    String
	     * @param strLength Md5Util#TO_LENGTH_32  Md5Util#TO_LENGTH_16
	     * @return String
	     */
	    public static String toMd5String(@NotNull String string, int strLength) {
	        try {
	            MessageDigest messageDigest = MessageDigest.getInstance("MD5");// 创建具有指定算法名称的信息摘要。
	            byte[] digest = messageDigest.digest(string.getBytes());//使用指定的 byte 数组对摘要进行最后更新，然后完成摘要计算。
	            if (strLength == TO_LENGTH_16) {
	                return new BigInteger(1, digest).toString(16).substring(8, 24);//转换16进制后截取中间的 16位
	            } else {
	                return new BigInteger(1, digest).toString(16);// digest 计算后的byte[] 转换为16进制
	            }
	        } catch (
	                NoSuchAlgorithmException e) {
	            e.printStackTrace();
	            return null;
	        }
	    }
	}

	//打印结果 
	//32位 MD5 : 202cb962ac59075b964b07152d234b70
	//16位 MD5 : ac59075b964b0715
	//32位 MD5 : 202cb962ac59075b964b07152d234b70

注：16位MD5值是有32位截取得来，安全性可想而知

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
