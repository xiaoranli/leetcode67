7、leetcode67. 二进制求和
==
解法一：
--  
思路：
--
    使用连个指针，从后往前加，保留进位，当短的字符串到头时，使用‘0’代替。
代码： 
--
<pre>

/**
 * @author lihe
 * @date 2019/10/15 20:42
 * @descriptor  67. 二进制求和
 */
public class AddBinary_67 {
    public static String addBinary(String a, String b) {
        StringBuilder builder = new StringBuilder();
        int i = a.length() - 1, j = b.length() - 1;
        int value = 0;//进位
        while (i >= 0 || j >= 0) {
            if(i<0){
                i=0;
                a = '0' + a.substring(1);
            }
            if(j<0){
                j=0;
                b = '0' + b.substring(1);
            }
            if (a.charAt(i) == '1' && b.charAt(j) == '1') {
                if (value == 1) {
                    builder.append(1);
                    value = 1;
                } else {
                    builder.append(0);
                    value = 1;
                }
                i--;j--;
            } else if (a.charAt(i) == '1' || b.charAt(j) == '1') {
                if (value == 1) {
                    builder.append(0);
                } else {
                    builder.append(1);
                }
                i--;j--;
            } else {
                if (value == 1) {
                    builder.append(1);
                    value = 0;
                } else {
                    builder.append(0);
                }
                i--;j--;
            }
        }
        if(value == 1)
            builder.append(1);
        return builder.reverse().toString();
    }
    public static void main(String[] args) {
       // String a = "1010";
       // String b = "1011";
        String a = "11";
        String b = "1";
        String s = addBinary(a, b);
        System.out.println(s);
    }
}
</pre>

解法二：
--  
思路：
--
    通过求%和求/分别得到进位和和，通过StringBuilder链接。
代码： 
--
<pre>

/**
 * @author lihe
 * @date 2019/10/15 20:42
 * @descriptor  67. 二进制求和
 */
public class AddBinary_67 {
    public static String addBinary2(String a, String b) {
        StringBuilder ans = new StringBuilder();
        int ca = 0; //是否进一位
        for (int i = a.length() - 1, j = b.length() - 1; i >= 0 || j >= 0; i--, j--) {
            int sum = ca;
            sum += (i >= 0 ? a.charAt(i) - '0' : 0);
            // 判断j>=0的含义是有可能两个数字长度不一致，如果j<0的话则将其当做0来处理，
            // 否则获取其值，也就是 b.charAt(j) - '0'
            sum += (j >= 0 ? b.charAt(j) - '0' : 0);
            ans.append(sum % 2);  //sum%2是在做二进制取模运算，比如sum=2，这时候将sum%2=0放入结果集中
            ca = sum / 2;// 这里是计算进位，比如sum=2，ca = 1，ca表示进位的意思，满2进1
        }
        //这一步表示是不是最后还有进位，比如1+1 = 10，10前面的1就是最后留存的进位，需要将其放进去
        ans.append(ca == 1 ? ca : "");
        return ans.reverse().toString();
    }
    public static void main(String[] args) {
       // String a = "1010";
       // String b = "1011";
        String a = "11";
        String b = "1";
        String s = addBinary(a, b);
        System.out.println(s);
    }
}
</pre>
