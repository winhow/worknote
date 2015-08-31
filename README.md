# worknote
学习笔记

1.fragment嵌套注意点：使用viewPager控件放置fragment当viewPager对象监听的时候不能用getActivity().getFragmentManager()，
需要用到getChildFragmentManager()的支持
