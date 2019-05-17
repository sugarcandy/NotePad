github有时候可能加载不出来图片，可以去csdn，内容一样，地址：https://mp.csdn.net/mdeditor/88996223#

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

修改插入(insert函数)语句：

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



 ## 2、添加搜索框

**日期：2019-4-7**

在主页添加一个搜索框，对note的title进行模糊查询。

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
        android:id="@+id/main_list"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <SearchView
            android:id="@+id/search_input"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginEnd="2dp"
            android:gravity="center_vertical"
            android:hint="@string/search"
            android:paddingLeft="5dip"
            android:singleLine="true">
        </SearchView>

        <LinearLayout
            android:id="@+id/view_method"
            android:layout_width="match_parent"
            android:layout_height="match_parent">
            <!--此处可以设置成listview布局或者瀑布流布局-->
            <ListView
                android:id="@+id/note_list"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="10dp">
            </ListView>
        </LinearLayout>

    </LinearLayout>

</LinearLayout>
```


2.  然后来到NotesList.java，这个类是继承于ListActivity，所以默认的界面就是只有一个列表，由于我们要添加搜素框，因此我们取消这个类的继承，而是将他还原成继承Activity，如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407231054754.png)

3.  继承的类改变了，相应的很多方法也是有所改变，但是其实修改的并不多。首先在onCreate()方法中设置布局文件并 手动获取ListView（之前由于是继承的ListActivity因此没有这一步）。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407231711727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

4.  将listview变量和adapter变量的定义直接放在Activity里，这样所有函数都能直接用他们，然后将所有飘红的getAdapter()函数改成adapter,反正飘红的地方都改，不漂红的不动他，然后你发现最后面有就是onListItemClick()函数的@override报错，是因为当前继承的Activity里面并没有这个方法，而这个函数的意义就是实现列表的item点击事件，很简单，将这个函数的内容复制，在onCreate()里面新建一个监听函数，将这个内容丢进去，完事把之前那个函数给注释掉，就ok了。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20190407232628126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

5.  接下来就是本次的核心，搜索的实现了。这个之前以为很难，结果做的时候发现太简单了吧。直接将listview获取数据的代码复制过去稍加修改就好了：

```
		searchView.setImeOptions(EditorInfo.IME_ACTION_SEARCH);//设置键盘回车为搜索键
//        searchView.setSubmitButtonEnabled(true);
        searchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
            @Override
            public boolean onQueryTextSubmit(String query) {

                return false;
            }

            @Override
            public boolean onQueryTextChange(String newText) {//监听搜索框的内容改变
//                text=editText.getText().toString();
                if(newText!=""){
                    selection=NotePad.Notes.COLUMN_NAME_TITLE+" like ?";//搜索条件
                    String []args={"%"+newText+"%"};
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

                    // Sets the ListView'sugar adapter to be the cursor adapter that was just created.
                    listView.setAdapter(adapter);
                }
                return false;
            }
        });

```
6.  搜索截图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019051223211740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

## 3、设置背景和字体颜色和大小

***日期 ：2019-4-15***

这个功能时针对每个文本来说的，所以是以菜单的形式存在于每个便签中，修改后将值存到数据库中，之后每次打开这个文件的时候就先从数据库加载的对应的背景和颜色。

首先设置菜单样式。
在editor_options_menu.xml的menu标签内添加如下内容
```
 <item android:id="@+id/menu_back"
        android:title="背景"
        android:icon="@drawable/ic_menu_compose">
        <menu>
            <item android:id="@+id/normal"
                android:title="标准" />
            <item android:id="@+id/literature"
                android:title="文艺"/>
            <item android:id="@+id/Antiquity"
                android:title="古风"/>
            <item android:id="@+id/Sugar"
                android:title="糖果"/>
            <item android:id="@+id/Stars"
                android:title="星辰大海"/>
        </menu>
    </item >
    <item android:id="@+id/font"
        android:title="字体">
        <menu>
            <item android:id="@+id/font_size"
                android:title="字体大小">
                <menu>
                    <item android:id="@+id/little"
                        android:title="小"/>
                    <item android:id="@+id/middle"
                        android:title="中"/>
                    <item android:id="@+id/big"
                        android:title="大"/>
                </menu>
            </item>
            <item android:id="@+id/font_color"
                android:title="字体颜色">
                <menu>
                    <item android:id="@+id/red"
                        android:title="红色"/>
                    <item android:id="@+id/black"
                        android:title="黑色"/>
                    <item android:id="@+id/green"
                        android:title="绿色"/>
                    <item android:id="@+id/blue"
                        android:title="蓝色"/>
                    <item android:id="@+id/purple"
                        android:title="紫色"/>
                </menu>
            </item>
        </menu>
    </item>
```

然后在设置每个菜单的相应事件：

在NotepadEditor的OnOptionsItemSelectd函数下添加如下：

```
			case R.id.Antiquity:
                mText.setBackground(getDrawable(R.drawable.antiquity));
                updateBackground(R.drawable.antiquity);
                break;
            case R.id.literature:
                mText.setBackground(getDrawable(R.drawable.literature));
                updateBackground(R.drawable.literature);
                break;
            case R.id.Sugar:
                mText.setBackground(getDrawable(R.drawable.sugar));
                updateBackground(R.drawable.sugar);
                break;
            case R.id.Stars:
                mText.setBackground(getDrawable(R.drawable.stars));
                updateBackground(R.drawable.stars);
                break;

            case R.id.little:
                mText.setTextSize(20);
                updateFontSize(20);
                break;
            case R.id.middle:
                mText.setTextSize(25);
                updateFontSize(25);
                break;
            case R.id.big:
                mText.setTextSize(30);
                updateFontSize(30);
                break;
            case R.id.black:
                mText.setTextColor(Color.BLACK);
                updateFontColor(Color.BLACK);
                break;
            case R.id.red:
                mText.setTextColor(Color.RED);
                updateFontColor(Color.RED);
                break;
            case R.id.green:
                mText.setTextColor(Color.GREEN);
                updateFontColor(Color.GREEN);
                break;
            case R.id.blue:
                mText.setTextColor(Color.BLUE);
                updateFontColor(Color.BLUE);
                break;
            case R.id.purple:
                mText.setTextColor(getColor(R.color.purple));
                updateFontColor(getColor(R.color.purple));
                break;
```
上面的updatexxx函数就不多说了，依葫芦画瓢，仿照他updatenote的写就好了。
现在菜单有了，然后就要设置每次启动的时候从数据库中加载数据了，说起数据库，别忘了在数据库中加入两个字段，分别是fontsize和fontsize，还要记得在Provider里面将这两个字段加入map。

然后就是运行前加载了，自然是将这个加载过程放在NotePadEditor的onCreate函数里面了，如下所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512225705768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512225723988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

看下效果图吧：

原背景和字体

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512230300904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

换个糖果背景：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512230320241.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512230336393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

字体设置为大:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512230442276.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

改变字体颜色（为了适应某些背景，有时候会看不清楚字,所以改变字体颜色就很必要）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512230509322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)


## 4、设置浮动按钮为新建
***日期：2019-5-25***

原生的新建太丑了，于是我想仿照自己手机上的记事本的样子，把新增键变成浮动按钮。

说干就干，修改note_list.xml，添加如下内容：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512232636405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

然后将原来的新增按钮的功能给他就好了：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512232921269.png)

效果图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512233147172.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

## 5、滑动菜单
***日期：2019-5-6***


觉得滑动菜单挺好看的，就想着做个试试看。

首先修改note_list.xml的样式，完整版如下（包括以上所有修改）:

```
<?xml version="1.0" encoding="utf-8"?>

<android.support.v4.widget.DrawerLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@drawable/pig"
        >
    <LinearLayout
        android:id="@+id/main_list"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <SearchView
            android:id="@+id/search_input"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginEnd="2dp"
            android:gravity="center_vertical"
            android:hint="@string/search"
            android:paddingLeft="5dip"
            android:singleLine="true">
        </SearchView>

        <LinearLayout
            android:id="@+id/view_method"
            android:layout_width="match_parent"
            android:layout_height="match_parent">
            <!--此处可以设置成listview布局或者瀑布流布局-->
            <ListView
                android:id="@+id/note_list"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="10dp">
            </ListView>
        </LinearLayout>

    </LinearLayout>

    <android.support.design.widget.FloatingActionButton
        android:id="@+id/floating"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_marginBottom="30dp"
        android:layout_marginRight="16dp"
        android:clickable="true"
        android:src="@drawable/add"
        app:backgroundTint="@color/aqua" />
    </FrameLayout>

    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:background="@drawable/lanhua"
        app:headerLayout="@layout/nav_header"
        app:menu="@menu/nav_menu">

    </android.support.design.widget.NavigationView>
</android.support.v4.widget.DrawerLayout>

```

滑动菜单由两部分组成：nav_header和nav_menu组成，分别如下：

nav_menu：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019051223384052.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
nav_header.xml：
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:padding="10dp"
    android:layout_height="180dp">

    <de.hdodenhof.circleimageview.CircleImageView
        android:id="@+id/iconimage"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_centerInParent="true"
        android:src="@drawable/pig"
        />

    <TextView
        android:id="@+id/mail"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:text="avdsda@163.com"
        android:textColor="#FFF"
        android:textSize="16sp"
        />
    <TextView
        android:id="@+id/name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@+id/mail"
        android:text="蔡虚鲲"
        android:textColor="#FFF"
        android:textSize="16sp"/>
</RelativeLayout>

```

在菜单的监听函数中添加监听：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512234344737.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019051223414424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

点击左上角的按钮，效果图如下：

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190512234502863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
 
上面的功能只能等有时间再说了。。。。
