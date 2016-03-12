# 선택위젯

# List View

##1. textView 하나를 List View의 item으로 만들기
![listView1.jpg]()
listView 생성
```XML
    <ListView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/listView"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true" />
```
listView inflation

```JAVA
public class MainActivity extends AppCompatActivity {

    ListView listView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listView=(ListView)findViewById(R.id.listView);

    }
```
inner class로 Adaptor 생성
```JAVA
class ListViewAdaptor extends BaseAdapter
    {
        String[] name={"양소현","유슬기","김정민","김동희","고민규"};

        @Override
        public int getCount() {
            return name.length;
        }

        @Override
        public Object getItem(int position) {
            return name[position];
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {

            TextView view = new TextView(getApplicationContext());

            view.setText(name[position]);
            view.setTextSize(60.0f);
            return view;
        }
```
listView에 Adaptor를 설정해 주기
```JAVA
public class MainActivity extends AppCompatActivity {

    ListView listView;
    ListViewAdaptor adaptor;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listView=(ListView)findViewById(R.id.listView);

        adaptor = new ListViewAdaptor();
        listView.setAdapter(adaptor);
    }

```

```JAVA


  
```
##2. 하나의 부분화면을 List View의 item으로 만들기
XML파일로 view group 만들기 (view 구성)

```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal" android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <ImageView

        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@drawable/flower" />
    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:layout_gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceSmall"
        android:text="Small Text"
        android:id="@+id/names"
        android:textSize="30dp"
       />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceSmall"
        android:text="Small Text"
        android:id="@+id/phones"
        android:textSize="30dp"
         />
        </LinearLayout>
</LinearLayout>

```
만든 view group을 화면에 붙이기
```JAVA
public class ListItemView extends LinearLayout
{
    public ListItemView(Context context) {
        super(context);

        init(context);
    }

    public ListItemView(Context context, AttributeSet attrs) {
        super(context, attrs);

        init(context);

    }

    public void init(Context context){

        LayoutInflater inflater = (LayoutInflater)context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        inflater.inflate(R.layout.listview_item, this, true);


    }

}
```
만든 TextView안에 들어가는 text설정 해주기

```JAVA
  public void init(Context context){

        LayoutInflater inflater = (LayoutInflater)context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        inflater.inflate(R.layout.listview_item, this, true);

        namesTextView = (TextView)findViewById(R.id.names);
        phonesTextView = (TextView)findViewById(R.id.phones);
     

    }
    
    public void setName(String name){
        namesTextView.setText(name);
    }

    public void setPhone(String phone){
        phonesTextView.setText(phone);
    }
```
Adaptor에 data입력, 보여줄 item 입력
```JAVA
  class ListViewAdaptor extends BaseAdapter
    {
        String[] name={"양소현","유슬기","김정민","김동희","고민규"};
        String[] phone={"010-1111-1111","010-2222-2222","010-3333-3333","010-4444-4444","010-5555-5555"};


        @Override
        public int getCount() {
            return name.length;
        }

        @Override
        public Object getItem(int position) {
            return name[position];
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {

            ListItemView view = new ListItemView (getApplicationContext());
            view.setName(name[position]);
            view.setPhone(phone[position]);


            return view;
        }
    }
```

-------------------------------------
데이터 따로 관리
-------------------------------------

```JAVA
public class MainActivity extends AppCompatActivity {

    ListView listView;
    ListViewAdaptor adaptor;

    String[] name={"양소현","유슬기","김정민","김동희","고민규"};
    String[] phone={"010-1111-1111","010-2222-2222","010-3333-3333","010-4444-4444","010-5555-5555"};

```
arrayList 객체를 따로 만들어서 data 관리
```JAVA
   class ListViewAdaptor extends BaseAdapter
    {
       
        ArrayList items =new ArrayList();
```

listitem에 대한 class 생성
```JAVA
public class ListItem {
    String name;
    String phone;

    public ListItem() {
     
    }

    public ListItem(String name, String phone) {
        this.name = name;
        this.phone = phone;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }
}
```
adaptor에 item설정해주기
```JAVA
 protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listView=(ListView)findViewById(R.id.listView);

        adaptor = new ListViewAdaptor();
        adaptor.addItem(new ListItem(name[0],phone[0]));
        adaptor.addItem(new ListItem(name[1],phone[1]));
        adaptor.addItem(new ListItem(name[2],phone[2]));
        adaptor.addItem(new ListItem(name[3],phone[3]));
        adaptor.addItem(new ListItem(name[4],phone[4]));



        listView.setAdapter(adaptor);


    }
```


##3. List View의 재활용

convertview 이용
```JAVA

     public View getView(int position, View convertView, ViewGroup parent) {

            ListItemView view = null;

            if(convertView ==null){
                view = new ListItemView (getApplicationContext());
            }else{
                view=(ListItemView) convertView;
            }
```


# Grid View

gridView 생성
```XML
    <GridView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/gridView"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:numColumns="3"/>
```
gridView inflation

```JAVA
public class MainActivity extends AppCompatActivity {

    GridView gridView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        gridView=(GridView)findViewById(R.id.gridView);

    }
```
inner class로 Adaptor 생성
```JAVA
class GridViewAdaptor extends BaseAdapter
    {
        String[] name={"양소현","유슬기","김정민","김동희","고민규"};

        @Override
        public int getCount() {
            return name.length;
        }

        @Override
        public Object getItem(int position) {
            return name[position];
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {

            TextView view = new TextView(getApplicationContext());

            view.setText(name[position]);
            view.setTextSize(30.0f);
            return view;
        }
```
gridView에 Adaptor를 설정해 주기
```JAVA
public class MainActivity extends AppCompatActivity {

    GridView gridView;
    GridViewAdaptor adaptor;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        gridView=(GridView)findViewById(R.id.gridView);

        adaptor = new GridViewAdaptor();
        gridView.setAdapter(adaptor);
    }

```

```JAVA

