---
layout: post
title: "কনটেস্ট টাইমে Algorithm Selection"
date: 2013-11-12 12:00:00
permalink: /algoselection.html
---
হুম, তুমি এখন কনটেস্টে আছো, হাতে প্রবলেম সেটটা পেয়েছো। প্রবলেমগুলার মধ্যে দিয়ে যাওয়ার সময় পেয়ে গেলে একটা পরিচিত প্রবলেম, তোমাদের মনে হচ্ছে এটা সল্ভ করতে পারবে। প্রবলেম পড়ার পরপরই তুমি এবং তোমার জিনিয়াস টীমমেট দুজন বাঘাবাঘা অ্যালগরিদম দাড় করায়ে ফেললে, তার মধ্যে থেকে সব থেকে সিম্পলটা সিলেক্ট করে কোড করার ট্রাই করতেছো। But there is a catch! তোমার অ্যালগরিদম কি আসলেই efficient??

ভালো কনটেস্ট প্রোগ্রামাররা এমন অ্যালগরিদম সিলেক্টশন বা বানানোর সময় প্রবলেমে দেওয়া ইনপুট দেখে অ্যালগরিদমটার কমপ্লেক্সিটিটা হিসাব করে নেয়। তার যথেষ্ট ভালো কারনও আছে। সাধারনত আমরা কনটেস্ট প্রোগ্রামাররা ধরে নি এখনকার কম্পিউটারগুলা 10<sup>7</sup> টি instructions মোটামুটি ১ সেকেন্ডে execute করতে পারে। এখন তুমি কনটেস্টে একটা অ্যালগরিদম তৈরী করে ফেললে যেটা কিনা ইনপুট সাইজের সাথে বিবেচনা করলে 10<sup>8</sup> বা তার বেশি হয়ে যাচ্ছে। কোড সাবমিট করলে জাজ তো তোমাকে TLE verdict দিতে বাধ্য হবেনই। তাই কোন অ্যালগরিদম চিন্তা করার আগে অবশ্যই মাথায় রাখতে হবে worst case scenario এর ব্যাপারটা। প্রবলেমে বলা থাকে সাধারনত যে testcases কতগুলা হবে এবং maximum input size কতগুলা থাকে। Worst case complexity = maximum test cases * maximum input size হবে (যদিও এই নিয়মেই সব প্রবলেমের কমপ্লেক্সিটি হিসাব করতে যেয়ো না,  সমস্যার বর্ণনায় কিছু তথ্য এক্সট্রা দেয়া থাকতে পারে)।

তো তুমি যখন তোমার worst case complexity পেয়ে গেলে তাইলে এখন খুব সহজেই টীমমেটদের সাথে গল্প করে most efficient এবং most simpler অ্যালগরিদমটি সিলেক্ট করতে পারবে। কমপ্লেক্সিটির কথা বিবেচনা না করে যদি কোড করা শুরু করো তাইলে দেখবে কোড-টোড করা শেষ, কিন্তু TLE খাচ্ছো বারংবার।

ইনপুট সাইজ এবং টেস্টকেইজ দেখে কনটেস্টের সময়ই কিছু সাম্ভাব্য অ্যালগরিদম guess করতে পারবে। যদিও সব সময় এমনটা হবে এমন কোনো গ্যারান্টি নাই। ইনপুট সাইজ দেখে সব থেকে খারাপ complexity এর সেসব অ্যালগরিদম ব্যবহার করতে পারবে ( অথচ যেগুলা ব্যবহার করলেও TLE খাবে না) সেটার একটা টেবিল দিলাম। চেষ্টা করবে যেন ইনপুট সাইজের সাথে এর সমতুল্য বা তার চে আরও efficient অ্যালগরিদম খুজে বের করে তারপর প্রবলেম সলভ করার।


<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<p><b>Maximum N</b></p>
</td>
<td><b>Maximum complexity can be applied</b></td>
<td><b>Algorithms</b></td>
<td><b>Possible data structures to use</b></td>
</tr>
<tr>
<td>1,000,000,000 and higher</td>
<td>log (n), sqrt (n)</td>
<td>binary search, ternary search, fast exponentiation, euclid algorithm
</td>
<td></td>
</tr>
<tr>
<td>10,000,000</td>
<td>n, n (log (log (n))), n log(n)</td>
<td>set intersection, Eratosthenes sieve, radix sort, KMP, topological sort, Euler tour, strongly connected components, 2sat
</td>
<td>disjoint sets, tries, hash_map, <a href="http://www.infoarena.ro/blog/rolling-hash">rolling hash</a> deque</td>
</tr>
<tr>
<td>1,000,000</td>
<td>n log n</td>
<td>sorting, divide and conquer, sweep line, Kruskal, Dijkstra
</td>
<td>segment trees, range trees, heaps, treaps, binary indexed trees, suffix arrays</td>
</tr>
<tr>
<td>100,000</td>
<td>n log<sup>2</sup> n</td>
<td>divide and conquer
</td>
<td>2d range trees</td>
</tr>
<tr>
<td>50,000</td>
<td>n<sup>1.585</sup>, n sqrt n</td>
<td>Karatsuba, square root trick
</td>
<td>two level tree</td>
</tr>
<tr>
<td>1000 - 10,000</td>
<td>n<sup>2</sup></td>
<td>largest empty rectangle, Dijkstra, Prim (on dense graphs)
</td>
<td></td>
</tr>
<tr>
<td>300-500</td>
<td>n<sup>3</sup></td>
<td>all pairs shortest paths, largest sum submatrix, naive matrix multiplication, matrix chain multiplication, gaussian elimination, network flow
</td>
<td></td>
</tr>
<tr>
<td>30-50</td>
<td>n<sup>4</sup>, n<sup>5</sup>, n<sup>6</sup></td>
<td>
</td>
<td></td>
</tr>
<tr>
<td>25 - 40</td>
<td>3<sup>n/2</sup>, 2<sup>n/2</sup></td>
<td>meet in the middle
</td>
<td>hash tables (for set intersection)</td>
</tr>
<tr>
<td>15 – 24</td>
<td>2<sup>n</sup></td>
<td>subset enumeration, brute force, dynamic programming with exponential states
</td>
<td></td>
</tr>
<tr>
<td>15 – 20</td>
<td>n<sup>2</sup> 2<sup>n</sup></td>
<td>dynamic programming with exponential states
</td>
<td>bitsets, hash_map</td>
</tr>
<tr>
<td>13-17</td>
<td>3<sup>n</sup></td>
<td>dynamic programming with exponential states
</td>
<td>hash_map (to store the states)</td>
</tr>
<tr>
<td>11</td>
<td>n!</td>
<td>brute force, backtracking, next_permutation
</td>
<td></td>
</tr>
<tr>
<td>8</td>
<td>n<sup>n</sup></td>
<td>brute force, cartesian product
</td>
<td></td>
</tr>
</tbody>
</table>

Keep coding… :)
