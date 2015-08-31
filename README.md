# worknote
学习笔记

1.fragment嵌套注意点：使用viewPager控件放置fragment当viewPager对象监听的时候不能用getActivity().getFragmentManager()，
需要用到getChildFragmentManager()的支持

现在好多应用流行一种布局。底部几个工具栏选项，上面也有类似tab的选项。
底部用RadioGroup控制fragment的切换。以上有五个fragment。
第一个fragment，代表着首页。首页又是一个类似tab的fragment，使用viewpager切换着两个fragment。

 private void InitViewPager(View parentView) {
       mPager = (ViewPager) parentView.findViewById(R.id.vPager);
       fragmentsList = new ArrayList<Fragment>();


       fragment1 = new SortHotFragment();
       fragment2 = new SortNewFragment();


       fragmentsList.add(fragment1);
       fragmentsList.add(fragment2);
       
       mPager.setAdapter(new MyFragmentPagerAdapter(getActivity().getSupportFragmentManager(), fragmentsList));
       mPager.setCurrentItem(0);
       mPager.setOnPageChangeListener(new MyOnPageChangeListener());
 }

一般根据往常的经验，如果要传入fragmentmanager,都是红色字体部分。
但是，这样会导致一个问题：数据丢失。
在fragment切换来回时，其他单个的fragment里面的数据不会丢失，而使用了viewpager的多个fragment切换的fragment会一团漆黑。

解决办法：
将红色字体部分，用getChildFragmentManager() 替换。
mPager.setAdapter(new MyFragmentPagerAdapter(getActivity().getChildFragmentManager(), fragmentsList));
mPager.setCurrentItem(0);
mPager.setOnPageChangeListener(new MyOnPageChangeListener());
