---
layout: post
title: "সি++ এর Priority Queue"
date: 2013-10-27 12:00:00
permalink: /cplusplus-priority-queue.html
---
Priority Queue হলো সি++ একটা STL যা প্রোগ্রামে ইনপুটগুলাকে সর্টেড অবস্থায় রেখে দেয়। অর্থাৎ এটা এক প্রকার অ্যারে, আরো ভাল ভাবে বলা যায় ভেক্টর যার উপাদানগুলা সর্টেড অবস্থায় থাকে। ডিফল্ট অবস্থায় এটা হাইয়ার টু লোয়ার প্রেসিডেন্সে (MAX priority queue) উপাদানগুলা সর্ট করে রাখে। তবে কাজের ভিন্যতার জন্য লোয়ার টু হাইয়ার (MIN priority queue) প্রেসিডেন্সেও সর্ট করা যায়। তবে এটা ডিফল্ট ভাবে করা থাকে না।

## MAX Priority Queue

```
#include <iostream>
#include <queue>
using namespace std;
main()
{
    priority_queue<int> pq;
    pq.push(1);
    pq.push(16);
    pq.push(6);
    pq.push(13);  
    while ( !pq.empty() )
    {
        cout << pq.top() << endl;
        pq.pop();
    }
}
```

এই কোডটা রান করলে আউটপুট হয়:

```
16
13
6
1
```

## MIN Priority Queue

মিনিমাম প্রায়োরিটি কিউ কাজ করাতে গেলে একটু কাজ নিজেদের করে নিতে হয়। অর্থাৎ কম্পেয়ারিং। একটা ক্লাস অথবা স্ট্রাকচার তৈরী করতে হয় যা উপাদানগুলাকে মিনিমাম প্রায়োরিটি অনুযায়ী সাজায়ে রাখে। তেমন কঠিন কিছুনা। জাস্ট এতটুকু লিখতে হয় এক্সট্রা:

```
struct compare
{
  bool operator()(const int& l, const int& r)
  {
      return l > r;
  }
};
```

এবং `priority_queue` টাইপ ভেরিয়েবল ডিক্লেয়ার করার সময় লিখতে হয়:

```
priority_queue<int, vector<int>, compare>pq;
```

অর্থাৎ কোডটা হবে:

```
#include <iostream>
#include <queue>
using namespace std;

struct compare
{
  bool operator()(const int& l, const int& r)
  {
      return l > r;
  }
};
main ()
{
    priority_queue<int,vector<int>, compare > pq;

    pq.push(1);
    pq.push(16);
    pq.push(6);
    pq.push(13);
    while ( !pq.empty() )
    {
        cout << pq.top() << endl;
        pq.pop();
    }
}
```

এই কোডটার আউটপুট হবে:

```
1
6
13
16
```

## Priority Queue on Custom Class

প্রায়োরিটি কিউ যদি আমরা কাস্টম ক্লাস অথবা স্ট্রাকচারের সাথে ইমপ্লিমেন্ট করতে চাই তাইলে আরো একটু বেশী কষ্ট করতে হয়। তবে কাজটা অনেক মজার। একটু দেখলেই বুঝতে পারবে।
আগে কোডটা একটু দেখে নাও:

```
#include <iostream>
#include <queue>

using namespace std;

struct hambaa {

    public:
    string apprnce;
    int age;
    hambaa( string c, int a)
    {
        apprnce = c;
        age = a;
    }
};

struct compare
{
  bool operator()(const hambaa& abc, const hambaa& def)
  {
      return abc.age > def.age;
  }
};

main()
{
    priority_queue < hambaa , vector<hambaa> , compare > pq;

    pq.push( hambaa ("bachhur",1)) ;
    pq.push( hambaa ("boro goru",16 ));
    pq.push( hambaa ("majhari goru", 6));
    pq.push( hambaa ("majhari boro goru", 10));
    while ( !pq.empty() )
    {
        cout << pq.top().apprnce<< " " << pq.top().age << endl;
        pq.pop();
    }
}
```

আউটপুট হবে:

```
bacchur 1
majhari goru 6
majhari boro goru 10
boro goru 16
``` 

এখানে একটা কাস্টম স্টাকচার (hambaa) তৈরী করা হয়েছে। যেখানে ২টা উপাদান আছে। আমরা চাই age অনুযায়ী সর্ট করতে। তাই আমরা compare স্ট্রাকচারে hambaa টাইপের abc এবং def নিয়েছি। এবং তা থেকে age অনুযায়ী রিটার্ন করেছি।  আর খেয়াল করলে দেখতে পারবে main() function এ যা করেছি সব আগের মতই।
আরও একটা কাজ করতে পারো। Operator Overloading করেও কাজটি অনেক সহজ হয়ে যায়। তাইলে তোমাকে আর এত ঝামেলা করে এইটুকু লেখা লাগবে না। 

```
priority_queue < hambaa , vector<hambaa> , compare > pq;
```

নিচের কোডে Operator Overloading করে কাজটা করেছি। কোডটা কতটা দেখতে সুন্দর লাগছে দেখতে পারো এখন।

```
#include <iostream>
#include <queue>

using namespace std;

struct hambaa
{
    string apprnce;
    int age;
    hambaa(string s, int nmbr){apprnce=s; age=nmbr;}
    bool operator < ( const hambaa& p) const { return p.age < age; }
};

main ()
{
    priority_queue <hambaa> pq;
    pq.push(hambaa("bachhur",1));
    pq.push( hambaa("boro goru",16 ));
    pq.push( hambaa("majhari goru", 6));
    pq.push(hambaa("majhari boro goru", 10));

    while ( !pq.empty() )
    {
        cout << pq.top().apprnce<< " " << pq.top().age << endl;
        pq.pop();
    }
}
```

এভাবে `priority_queue` নিয়ে অনেক মজার মজার কাজ করতে পারবে, সর্টেড লিস্টের জন্য। কিপ কোডিং :)
