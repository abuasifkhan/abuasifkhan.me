---
layout: post
title: "Extended Euclidean Algorithm এবং একটুখানি Modular Multiplicative Inverse"
date: 2014-07-02 12:00:00
categories: Algorithm
permalink: /algorithm/extended-euclidean-algorithm.html
---
GCD (Greatest Common Divisor) বের করার জন্য হয়তো সবাই ইউক্লিডের পদ্ধতি ব্যবহার করেই দেখেছ। এটা আমার জানা মনে দুটি সংখ্যার GCD বের করার সব থেকে সহজ এবং efficient উপায়। যাহোক Extended Euclidean Algorithm জানার জন্য এই পদ্ধতিটাই কাজে লাগে। এখন দেখাই আগে কিভাবে GCD বের করতে হয় যদিও প্রায় সবার জানা আছে।<!--more-->

<strong>Python Code:</strong>
```
def GCD(x, y):
    if(y==0):
        return x
    return GCD(y, x%y)
```
<strong>C++ Code:</strong>

Recursive Method:
```
int GCD(int x, int y)
{
  if (y==0) return x;
  return GCD(y,x%y);
}
```
<strong>Iterative Method:</strong>
```
int GCD(int x, int y)
{
  while (y != 0)
  {
    int temp = y;
    y = x % y;
    x = temp;
  }
  return x;
}
```
এবার কাজে আসি। প্রথমে দেখা দরকার কিভাবে Extended Euclid Algorithm কাজ করে। তার আগে তোমাদেরকে বলবো Extended Euclid Method দিয়ে হাতে-কলমে কিভাবে সমীকরন সমাধান করা যায় সেটা দেখে আসতে। এজন্য এই <a title="Euclid Method" href="http://www.abuasifkhan.me/2013/07/extended-euclid-method/" target="_blank">লিংকে </a>একটু ঢু মেরে আসো।

কাজে ফিরে আসি। Extended Euclid এর মাধ্যমে সমাধান করার জন্য সমীকরনটা অবশ্যই এমন কাঠামোর হতে হবে: <strong>ax + by = GCD(a, b)</strong>

অর্থাৎ যদি ডান পাশে যে সংখ্যা থাকবে সেটা অবশ্যই a, b এর GCD হইতে হবে। কেবল সেক্ষেত্রেই আমরা x এবং y এর মান বের করতে পারবো Extended Euclidean Algorithm এর মাধ্যমে।

এখন একটা উদাহরন দিলে বুঝবে সুত্রটা কেমন সময় ব্যবহার করা যায়। ধর এক একটা আম এবং কলার মুল্য যথাক্রমে ১৫ এবং ৭ টাকা। একজন মহিলা ৮৫০ টাকা দিয়ে তাইলে কতটা আম এবং কলা কিনতে পারবে? এক্ষেত্রে এই সুত্রটা ব্যবহার করা যেতে পারে। অর্থাৎ 15x+7y=850. তবে এটা কেবল উদাহরন। Extended Euclid Algorithm এর জন্য ডান পাশের ধ্রুবক মানটি অবশ্যই (15, 7) এর গসাগু হইতে হবে।

Extended Euclid এর সুত্রটা এই form এ কাজ করে: <strong>r<sub>i</sub> = ax<sub>i</sub> + by<sub>i</sub> ……(1)</strong>

এভাবে r<sub>i</sub> এর মান প্রতি ধাপে ধাপে বাড়িয়ে পরবর্তি r এর মান বের করা হয়।

এখন প্রথমেই জানা দরকার দুটি সংখ্যার ভাগশেষ বের করার সুত্র :

<strong>X % Y = X – floor(X/Y)*Y</strong>

এই সুত্রটা থেকে আমরা স্বাভাবিকভাবেই লিখতে পারি:

<strong>r<sub>i</sub> = r<sub>i-2</sub> - floor(r<sub>i-2</sub> / r<sub>i-1</sub> ) * r<sub>i-1</sub></strong>

এখন ধরি, <strong>q<sub>i</sub> </strong>= <strong>floor(r<sub>i-2</sub> / r<sub>i-1</sub> )</strong>

অর্থাৎ, <strong>r<sub>i</sub> = r<sub>i-2</sub> - <strong>q<sub>i</sub> </strong>* r<sub>i-1</sub></strong>

এখন (1) নং সমীকরন থেকে যদি<strong> r</strong><sub>i-1</sub> এবং<strong> r</strong> <sub>i-2</sub> মান উপরের সমীকরনে বসাও তাইলে পাবে:

<strong> r<sub>i</sub> = (ax<sub>i-2</sub> + by<sub>i-2</sub>) – q<sub>i</sub> (ax<sub>i-1</sub> + by<sub>i-2</sub>)</strong>

<strong> =&gt; r<sub>i</sub> = a (x<sub>i-2</sub> - q<sub>i</sub>x<sub>i-1</sub>) + b (y<sub>i-2</sub> – q<sub>i</sub> y<sub>i-2</sub>) </strong> ( a এবং b এর common term গুলা একসাথে লিখে পাই)<strong>
</strong>

এখানে <strong>x<sub>i</sub>=(x<sub>i-2</sub> - q<sub>i</sub>x<sub>i-1</sub>) …… (2) এবং y<sub>i</sub>= (y<sub>i-2</sub> – q<sub>i</sub> y<sub>i-2</sub>) ….. (3)</strong>

r<sub>i</sub> এবং r<sub>2</sub> initial মান আমরা এভাবে পাই:

<strong> r<sub>1</sub> = a(1) + b(0) = a // x=1, y=0</strong>

<strong> r<sub>2</sub> = a(0) + b(1) = b // x=0, y=1</strong>

r<sub>1</sub> এবং r<sub>2 </sub>এর মান তো পেয়ে গেলাম এখন শুধু q<sub>i</sub> , r<sub>i</sub> , x<sub>i</sub> , y<sub>i</sub> এর মানগুলা লুপ ঘুরিয়ে কেবল আপডেট করব এবং a%b==0 হইলে অর্থাৎ r এর মান ০ হইলে লুপের কাজ শেষ করে দিব। এখন একটা উদাহরন দিলে ভাল ভাবে বুঝতে পারবে আরও। ধর, a=23 এবং b=120.



<strong>Initial Step:</strong>
```
     r1 = a(1) + b(0) = 120 x 1 + 23 x 0 = 120 // x=1, y=0
     r2 = a(0) + b(1) = 120 x 0 + 23 x 1 = 23   // x=0, y=1
```
<strong>Iterative Steps:</strong>
```
Step 1:
          a=23, b=120 ,  r3 = 120 % 23 = 5 ,  q3 = 120 / 23 = 5
          x3 = 0 – 5*1 ,  y3 = 1 – 5*0     /// From (2) and (3)

Step 2:
         a=5, b=23 ,  r4 = 23 % 5 = 3 ,  q4 = 23 / 5 = 4
         x4 = 1 – 4*(-5) = 21 ,  y4 = 0 – 4*1 = -4

Step 3:
         a=3, b=5 ,  r5 = 5 % 3 = 2 ,  q5 = 5 / 3 = 1
         x5 = -5 – 1*21 = -26 ,  y5 = 1 – 1 * (-4) = 5

Step 4:
         a=2, b=3 ,  r6 = 3 % 2 = 1 ,  q6 = 3 / 2 = 1
        x6 = 21 – 1*(-26) = 47 ,  y6 = -4 – 1 * 5 = -9
```
লুপের সমাপ্তি, কারন পরের ধাপে r এর মান 0 হবে।

উপরের উদাহরন থেকে আমরা কিছু তথ্য খুজে পেতে পারি। যেমন যদি x এর মান পজিটিভ হয় তাইলে y নেগেটিভ এবং y এর মান পজিটিভ হলে x নেগেটিভ।

আবার যদি GCD(a, b) = 1 হয় অর্থাৎ যদি a, b co-prime হয়ে থাকে তাইলে x হবে (a modulo b) এর Modular Multiplicative Inverse, এবং y হবে (b modulo a) এর Modular Multiplicative Inverse.

অর্থাৎ উপরের উদাহরনে -9 হল 120 modulo 23 এর multiplicative inverse এবং 47 হবে 23 modulo 120 এর multiplicative inverse.

Extended Euclid ফাংশনের কোড:

<strong>Iterative Method:</strong>
```
int Extended_Euclid(int A, int B, int *X, int *Y)
{
    int x, y, u, v, m, n, a, b, q, r;
    ///* B = A(0) + B(1) */
    x = 0;  /// x [i-2]
    y = 1;  /// y [i-2]
    ///* A = A(1) + B(0) */
    u = 1;  /// x[i-1]
    v = 0;  /// y[i-1]
    a = A;
    b = B;

    while ( a != 0 )
    {
        ///* b = aq + r and 0 &lt;= r &lt; a */
        q = b / a;

        /// GCD function
        r = b % a;
        b = a;
        a = r;

       /// /* r = A(x - uq) + B(y - vq) */ ///
        m = x - (u * q); /// m = x[i] = (x - uq)
        n = y - (v * q);  /// n = y[i] = (y - vq)
        x = u;  /// updating x[i-1] = x[i-2]
        y = v;  /// updating y[i-1] = y[i-2]
        u = m;  /// updating x[i] = x[i-1]
        v = n;  /// updating y[i] = y[i-1]
    }

    ///* Ax + By = gcd(A, B) */
    *X = x;
    *Y = y;

    return b;
}
```
<strong>Recursive Method:</strong>
```
int extendedEulid(int a, int b)
{
    if(b==0)
    {
        x=1; y=0; d=a;  /// some extensions
        return a;
    }

    int ret = extendedEulid(b, a%b);   /// GCD function
    int x1 = y;         /// some extensions
    int y1 = x - (a/b) *y;
    x = x1;
    y = y1;

    return ret;
}
```
<strong>Python Code:</strong>
```
def ExtendedEuclid(a, b):
    x, xi = 0, 1
    y, yi = 1, 0

    while b&gt;0:
        q = int(a / b)
        a, b = b, a % b
        x, xi = xi - q*x, x
        y, yi = yi - q*y, y

    return (xi, yi, a)
```
যথাসম্ভব ব্যাখ্যা করে লেখার চেষ্টা করেছি। ভুলত্রুটি থাকাটা স্বাভাবিক। সংশোধন অথবা কোন সমস্যা থাকলে কমেন্টে জানাও এবং keep coding... :)
