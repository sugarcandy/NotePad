
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

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403152704994.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

修改value的值，将关于modifycation_date的这个if语句注释掉，不判断直接put。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403151426212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

4. 更改NoteEditor.java文件:
 
 更改更新的时间，把原来的获取时间戳的语句删掉。
 
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019040315241523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

5. 运行图：

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403151620960.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
 
 
 ## 添加搜索框

**日期：2019-4-7**

首先，我的目的是在进去的首页加一个搜索框达到搜索的效果，然后乘着有空就先做个搜索框备着，如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407230542228.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

1.  首先新建一个布局文件note_list.xml,如下：

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/search"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <EditText
            android:id="@+id/search_input"
            android:layout_width="0dp"
            android:layout_height="44dp"
            android:layout_marginEnd="2dp"
            android:layout_weight="1"
            android:gravity="center_vertical"
            android:hint="@string/search"
            android:paddingLeft="5dip"
            android:textSize="20dp" />

        <Button
            android:id="@+id/toSearch"
            android:layout_width="wrap_content"
            android:layout_height="44dp"
            android:layout_marginTop="2dp"
            android:text="Search" />
    </LinearLayout>

    <ListView
        android:id="@+id/note_list"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

    </ListView>

</LinearLayout>
```


2.  然后来到NotesList.java，这个类是继承于ListActivity，所以默认的界面就是只有一个列表，由于我们要添加搜素框，因此我们取消这个类的继承，而是将他还原成继承Activity，如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407231054754.png)

3.  继承的类改变了，相应的很多方法也是有所改变，但是其实修改的并不多。首先在onCreate()方法中设置布局文件并 手动获取ListView（之前由于是继承的ListActivity因此没有这一步）。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407231711727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

4.  将listview变量和adapter变量的定义直接放在Activity里，这样所有函数都能直接用他们，然后将所有飘红的getAdapter()函数改成adapter,反正飘红的地方都改，不漂红的不动他，然后你发现最后面有就是onListItemClick()函数的@override报错，是因为当前继承的Activity里面并没有这个方法，而这个函数的意义就是实现列表的item点击事件，很简单，将这个函数的内容复制，在onCreate()里面新建一个监听函数，将这个内容丢进去，完事把之前那个函数给注释掉，就ok了。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407232628126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
5.  接下来就是本次的核心，搜索的实现了。这个之前以为很难，结果做的时候发现太简单了吧。简陋版的直接对按钮事件进行一个click事件就好了。事件里面就是重新定义一个cursor，然后对listview重新绑定一个adapter。代码如下：

```
search.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                text=editText.getText().toString();
                if(text!=""){
                    selection=NotePad.Notes.COLUMN_NAME_TITLE+" like ?";
                    String []args={"%"+text+"%"};
                    selectionArgs=args;
                    cursor = managedQuery(
                            getIntent().getData(),            // Use the default content URI for the provider.
                            PROJECTION,                       // Return the note ID and title and time for each note.
                            selection,                             // No where clause, return all records.
                            selectionArgs,                             // No where clause, therefore no where column values.
                            NotePad.Notes.DEFAULT_SORT_ORDER  // Use the default sort order.
                    );


                    String[] dataColumns = {
                            NotePad.Notes.COLUMN_NAME_TITLE,
                            NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE  //显示时间戳
                    };


                    int[] viewIDs = {
                            android.R.id.text1,
                            R.id.time
                    };

                    adapter = new SimpleCursorAdapter(
                            NotesList.this,                             // The Context for the ListView
                            R.layout.noteslist_item,          // Points to the XML for a list item
                            cursor,                           // The cursor to get items from
                            dataColumns,
                            viewIDs
                    );

                    // Sets the ListView's adapter to be the cursor adapter that was just created.
                    listView.setAdapter(adapter);
                }
            }
        });

```
6.  搜索截图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411223127438.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
