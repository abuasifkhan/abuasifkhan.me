---
layout: post
title: "সি++ দিয়ে বিভিন্নরকম Conversions"
date: 2015-03-28 12:00:00
permalink: /cplusplus-conversions.html
---
প্রোগ্রামিং করার সময় প্রায়ই অনেকরকম কনভার্সনের দরকার পড়ে। সি++ এ অনেকভাবেই এবং অনেক সহজে এসব কনভার্সন করা যায়। যদিও আমার personal favorite `stringstream`. কিছু উদাহরন দিচ্ছি নিচে, আশা করি ব্যাখ্যাও করা লাগবে না। :)

```
///int to string
stringstream ss;
int a = 1234;
ss<<a;  /// stream in
string s1;
ss>>s1; /// stream out
cout<<s1<<endl;

///string to int
ss.clear();
string s = "1234"
ss<<s;
int b;
ss>>b;
cout<<b<<endl;

/// char* to string
ss.clear();
char somechars[10] = "ruet cse";
ss<<somechars;
string somestrings;
ss>>somestrings;
cout<<somestrings<<endl;

/// string to char*
ss.clear();
somestrings = "ruet cse";
ss<<somestrings;
ss>>somechars;
cout<<somechars<<endl;
```

আশা করি বুঝতে অসুবিধা হয় নাই। যদি কোনরকম সমস্যা অথবা ভুল থাকে তাইলে কমেন্ট করে জানাবে অবশ্যই।
