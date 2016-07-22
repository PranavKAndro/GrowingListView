#  GrowingList View

## Welcome to the GrowingListView wiki!

### Synopsis:
### Introduction
### Problem statement
### How to include in your project
### How to use this view

## GrowingListView
## Introduction: 

The growing list view is a kind of list view that resembles the recycler view with the same style of the recycler view adapter. This library grows in the height as the height of the items inside dynamically.

## Problem Statement:

The recycler view or the list view doesn't grow in size dynamically while being inside the scroll view. Also setting the height dynamically to the items height is programmatically achievable but it behaves differently on different devices.

The growing list view is built to resolve this issue. Include the view provided by the library and include the adapter class in the project and set it to the list and see the magic that the list will be growing in size dynamically with the height of the height.

## How to include in your project:

1. Just download the .aar file from the following link : https://github.com/PranavKAndro/GrowingListView.
2. Include the .aar file into the project by new-->module-->import .aar module in the android studio.
3. Sync the project with the gradle.

## How to use this view:

In the layout xml include the growing list view as follows,

    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"`
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="pranav.com.growinglistimpl.MainActivity">

    <pranav.com.growinglistview.ui.GrowingListView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/growingsample">

    </pranav.com.growinglistview.ui.GrowingListView>
    </RelativeLayout>


Then create Adapter class extending the GrowingListAdapter,

    public class adapter extends GrowingListAdapter {

    ArrayList<String> strings ;
    public adapter(Context context,ArrayList<String> items) {
        super(context);
        strings=items;
    }
    
    @Override
    public int getItemCount() {
        return strings.size();
    }

    @Override
    public GrowingListViewHolder OnCreateViewHolder(Context context) {
        View v = LayoutInflater.from(context).inflate(R.layout.itemview,null,false);
        adapter.viewHolder holder = new viewHolder(v);
        return holder;
    }

    @Override
    public void OnBindViewHolder(int i, GrowingListViewHolder growingListViewHolder) {

        adapter.viewHolder holder = (adapter.viewHolder)growingListViewHolder;
        holder.sanple.setText(strings.get(i));

    }

    // create a view holder class 
    class viewHolder extends GrowingListViewHolder
    {
        TextView sanple;
        public viewHolder(View itemView) {
            super(itemView);
            sanple = (TextView) itemView.findViewById(R.id.textView);
        }
    }
    }


In the mainActivity set the adapter to the growing list view as follows,

    public class MainActivity extends AppCompatActivity
    {
        @Override
        protected void onCreate(Bundle savedInstanceState) 
        {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            GrowingListView growingListView = (GrowingListView) findViewById(R.id.growingsample);
            ArrayList<String> strings = new ArrayList<>();
            strings.add("i am 0");
            strings.add("i am 1");
            strings.add("i am 2");
            strings.add("i am 3");
            strings.add("i am 4");
            strings.add("i am 5");
            strings.add("i am 6");
            adapter adapterq = new adapter(this,strings);
            growingListView.setAdapter(adapterq);
            strings.add("i am 7");
            adapterq.notifyDataSetChanged();
            strings.add(0,"I am changed at postion 0");
            adapterq.notifyDataItemChanged(0);
            
        }

     }

NotifyDataSetChanged() -- call this function once if you change the data in the list to reflect to the UI.

notifyDataItemChanged(int position) -- call this function to change the item at the particular position.

To use the item click listener.
Follow the below procedure,

    growingListView.setOnClickListener(new OnGrowingListItemClickListener()
    {
       @Override
       public void onClick(View view, int i) {
           Toast.makeText(MainActivity.this, "Hello i am clicked"+i, Toast.LENGTH_SHORT).show();
       }
     });

Enjoy using the GrowinListView !!! :+1: 
