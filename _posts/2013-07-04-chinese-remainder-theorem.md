---
layout: post
title: Chinese Remainder Theorem
date: 2013-07-04 12:00:00
categories: Algorithm
---
<a title="উইকি" href="http://en.wikipedia.org/wiki/Chinese_remainder_theorem" target="_blank"><strong>Chinese Remainder Theorem</strong></a> একটা খুবই interesting theorem. প্রথমে বলি এটা কোন কোন প্রবলেমগুলার সাথে deal করতে পারে। এটা জানলেই বুঝবে কেন এটাকে এতটা interesting বলতেছি। আগেই বলে রাখি, এই থিওরেমটি শিখতে এবং প্রোগ্রামে কোড করতে হলে অবশ্যই <a title="উইকি" href="http://en.wikipedia.org/wiki/Modular_multiplicative_inverse" target="_blank"><strong>Modular Multiplicative Inverse</strong></a> কিভাবে Extended Euclid Method এর সাহায্যে বের করতে হবে সেটা জেনে রাখা দরকার( এজন্য এই <a href="http://www.abuasifkhan.me/2013/07/extended-euclidean-algorithm/" target="_blank">লিংকে </a>চলে যাও)। যদিও খাতা-কলমে কিভাবে Modular Multiplicative Inverse বের করা যায় সেটা শেখাবো এখানে। তারপরও কোড করার জন্য ইউক্লিডের মেথডটা শিখে রাখার জন্য বলবো সবাইকে।<!--more-->

এখন আমরা জানি যে: <strong>5 (mod 8)</strong> <strong>≡ 5</strong> আবার <strong>13 (mod 8) ≡ 5, 21 (mod 8) ≡ 5</strong>. এখন যদি তোমাকে একটা শর্ত দিয়ে দেয়া হয় যে <strong>z (mod 3)  ≡ 2</strong> হতে হবে। এখানে <strong>z = {5, 13, 21}</strong>, তাইলে শর্তটা দেখা যাচ্ছে মোটামুটি <strong>5</strong> এর জন্য সত্য তবে <strong>13</strong> এবং <strong>21</strong> এর জন্য সত্য হচ্ছে না। অর্থাৎ এখানে একমাত্র <strong>5</strong> ই সঠিক মান যেটা সকল শর্ত পুরন করতেছে। এই ধরনের সমস্যার সমাধান Chinese Reminder Theorem দিতে পারে। অর্থাৎ একাধিক modular condition থাকবে যেটা থেকে এমন সব সঠিক মান বের করতে হবে যা সকল দেয়া শর্ত মেনে চলবে। অবশ্য এক্ষেত্রে উত্তর অসীম সংখ্যক হইতে পারে। সেগুলাও বের করার উপায়ও এই থিওরেমটি দিয়ে দেয়। :)

এখন কাজে আসি, একটা উদাহরন সমাধান করার মাধ্যমে থিওরেমটা শেখার চেষ্টা করি। কিছু শর্ত আছে ধরে নিলাম:<strong>
</strong><strong>Z = 4 (mod 5)</strong>

<strong>Z = 6 (mod 7)</strong>

<strong>Z = 3 (mod 11)</strong>

এই শর্তগুলা সিদ্ধ করে এমন সব <strong>Z</strong> এর মান আমাদের বের করতে হবে। তো প্রথমে বলে রাখি এখানে রিমাইন্ডারগুলা হবে <strong>b</strong><sub>i</sub> এর মান। অর্থাৎ, <strong>b = {5, 7, 11}</strong> এবং <strong>c<sub>i </sub></strong>হবে প্রাপ্তমানগুলা অর্থাৎ <strong>c = {4, 6, 3}</strong>. প্রথমে যেটা করতে হবে সেটা হলো <strong>B (big B)</strong> এর মান বের করা। এটার সুত্র হলো:<strong></strong>

&nbsp;

যার মানে হলো সকল <strong>b<sub>i</sub> </strong>এর গুণফলগুলা হলো<strong> B (big B)</strong> এর মান। এক্ষেত্রে,

<b>B = 5x7x11 = 385</b>

এবার আমাদের কাজ হলো <strong>B</strong><sub>i </sub>এর মান বের করা। এটার সূত্র হলো:

<b>B<sub>i</sub> = B ÷ b<sub>i</sub></b>

অর্থাৎ,

<b>B<sub>1</sub> = 385/5 = 77</b>

<b>B<sub>2</sub> = 385/7 = 55</b>

<b>B<sub>3</sub> = 385/11 = 35</b>

চায়নিজ রিমাইন্ডার থিওরেম থেকে Z এর মান বের করার সূত্রটা হলো:

<b>Z = B<sub>1</sub>X<sub>1</sub>c<sub>1 </sub>+ B<sub>2</sub>X<sub>2</sub>c<sub>2 </sub>+ B<sub>3</sub>X<sub>3</sub>c<sub>3 </sub>+ </b><b>…</b><b> + B<sub>n</sub>X<sub>n</sub>c<sub>n</sub></b>

এই উদাহরনটার ক্ষেত্রে:

<b>Z = B<sub>1</sub>X<sub>1</sub>c<sub>1 </sub>+ B<sub>2</sub>X<sub>2</sub>c<sub>2 </sub>+ B<sub>3</sub>X<sub>3</sub>c<sub>3</sub></b>

এখানে আমাদের <strong>B<sub>i </sub></strong>এবং <strong>c</strong><sub>i</sub> এর মান আগে থেকেই জানা। তবে এখানে<strong> X</strong><sub>i </sub>টা আবার কি জিনিস?? হুম, এই কাজেই আমাদের লাগবে Extended Euclid. এটা শেখার জন্য <a href="http://www.abuasifkhan.me/2013/07/extended-euclidean-algorithm/">লিংকে</a> যাও (যদিও লেখার শুরুতে একবার দিয়েছি লিংকটা)। এখানে আমরা <strong>B<sub>i</sub> </strong>এবং <strong>b</strong><sub>i</sub> এর modular multiplicative inverse বের করবো। এ দুইটা মানের উপর Extended Euclid চালালে আমরা যে <strong>X</strong> এর মানটা পাই সেটাই এখানে <strong>X<sub>i</sub> </strong>এর মান।

এখন

<b>B<sub>1</sub>X<sub>1</sub></b><b> </b><strong>≡</strong><strong> </strong><strong>1 (mod b<sub>1</sub>)</strong><strong></strong>

<strong>=</strong><b>&gt; 77 </b><b>X<sub>1</sub></b><strong> ≡ 1 (mod 5)</strong><strong></strong>

<strong>=&gt; (77-80) </strong>X<sub>1</sub> <strong>≡ 1 (mod 5)</strong><strong>                   [ 4</strong><strong> এর গুণিতক</strong><strong> </strong><strong>দ্বারা </strong><strong>5 </strong><strong>কে বিয়োগ করে</strong><strong> </strong><strong>]</strong>

<strong>=&gt; (-3) X<sub>1</sub> ≡ 1 (mod 5)</strong>

<strong>=&gt; (-3) X<sub>1 </sub>≡ 6 (mod 5)            </strong><strong>                        [ 1 (mod 5) ≡ 6 (mod 5) ]</strong>

<strong>সুতরাং, </strong><b>X<sub>1</sub></b><b> </b><strong>= -2</strong>

<strong>আবার,</strong><strong></strong>

<strong>B<sub>2</sub> X<sub>2</sub> ≡</strong><strong> </strong><strong>1 (mod b<sub>2</sub>)</strong>

<strong>=</strong><b>&gt; 55 </b><b>X<sub>2</sub></b><b> </b><strong>≡ 1(mod 7)</strong><strong></strong>

<strong>=&gt; (55-56) X</strong><sub>2</sub> <strong>≡ 1 (mod 7)</strong><strong>                               [ 55 </strong><strong>থেকে </strong><strong>7 </strong><strong>এর গুণিতক বিয়োগ করে</strong><strong> </strong><strong>]</strong>

<strong>=&gt; (-1) X<sub>2</sub> ≡ 1 (mod 7)</strong><strong></strong>

<strong>সুতরাং, X<sub>2</sub> = -1</strong><strong></strong>

<strong>এভাবেই, </strong><strong>35 X<sub>3</sub> ≡ 1 (mod 11)</strong><strong> </strong><strong>থেকে পাই, </strong><strong>X<sub>3</sub> = -5</strong><strong>. X </strong><strong>এর মানগুলার অনেক হতে পারে, তবে </strong><strong>Extended Euclid Method </strong><strong>ব্যবহার করলে এই মানগুলাই পাওয়া যায়।</strong>

এখন Chinese Reminder Theorem এর আসল সূত্রটাতে আসি:

<b>Z = B<sub>1</sub>X<sub>1</sub>c<sub>1 </sub>+ B<sub>2</sub>X<sub>2</sub>c<sub>2 </sub>+ B<sub>3</sub>X<sub>3</sub>c<sub>3</sub></b>

<b>=&gt; Z = 77x(-2)x4 + 55x(-1)x6 + 35x(-5)x11 = -1471</b>

যে মানটা পাইলাম সেটা দিয়ে দেয়া শর্তগুলার সবকয়টি সিদ্ধ হবে। সুতরাং এটা একটা উত্তর। তবে আমি আগেই বলেছি অসীম সংখ্যক উত্তর থাকবে এই সমস্যাটার জন্য। তাইলে আমরা সেগুলা কিভাবে বের করবো? খুবই simple, প্রাপ্ত <strong>B (big B)</strong> এর মানের যেকোনো গুণিতক দিয়ে <strong>Z</strong> এর প্রাপ্ত মানের সাথে যোগ অথবা বিয়োগ দিলেই হয়ে গেলো। অর্থাৎ <b>( 4x385 - (-1471) ) = 69</b>, এটাও একটি সঠিক মান। এভাবে তুমি যেকোনো লিমিটের জন্য একটা সাম্ভাব্য মান খুজে পেতে পারবে। এখন নিচের উদাহরনটি সমাধান করার ট্রাই করো:

<b>Z = 3 (mod 8)</b>

<b>Z = 1 (mod 9)</b>

<b>Z = 4 (mod 11)</b>

Keep coding... :)

&nbsp;
