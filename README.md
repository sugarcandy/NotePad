@[toc]
## 1、添加时间显示

**日期：2019-4-3**

 1. 更改noteslist_item.xml文件为：

```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_height="wrap_content"
    android:layout_width="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@android:id/text1"
        android:layout_width="match_parent"
        android:layout_height="?android:attr/listPreferredItemHeight"
        android:textAppearance="?android:attr/textAppearanceLarge"
        android:gravity="center_vertical"
        android:paddingLeft="5dip"
        android:singleLine="true"
    />

    <!--这是显示时间戳的行-->
    <TextView
        android:id="@+id/time"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="15dp"
        android:gravity="center_vertical"/>
</LinearLayout>

```

 2. 更改NotesList.java文件，如下图所示：

 更改查询项
  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403150353230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
  
 更改匹配项
    
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403150253819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

3. 更改NotePadProvider.java，如图：

 修改建表语句
 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403150641981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

修改插入语句：

删掉原来的 Long now=.......这句。

添加图片中红圈语句。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019040315083196.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

修改value的值，将关于modifycation_date的这个if语句注释掉，不判断直接put。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403151426212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

4. 更改NoteEditor.java文件:
 
 更改更新的时间，把原来的获取时间戳的语句删掉。
 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403151148401.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

5. 运行图：

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403151620960.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
