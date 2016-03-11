# 선택위젯

# List View

##1. textView 하나를 List View의 item으로 만들기

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

##3. List View의 재활용

# Grid View
