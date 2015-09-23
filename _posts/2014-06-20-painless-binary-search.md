---
layout: post
title: Painless Binary Search
date: 2014-06-20 12:00:00
categories: Algorithm
---
এত সহজভাবে নিয়ো না ব্যাপারটা। বাইনারী সার্চ যতটা সহজ ভাবছো ততটা সহজ আসলে এটা না, ডিবাগ করতে গেলে জান বের হয়ে যাওয়ার উপক্রম হয় মাঝে মাঝে সবারই। এখনও ৯০% কোডাররা এটা on sight কোড করতে গেলে বিভিন্ন সমস্যায় পড়ে যায়। এতক্ষনে হয়তো তোমারও মনে পড়ে যাওয়ার কথা যে বাইনারী সার্চ কোড করতে তোমারও কতবার গুগল করে বা বই দেখে ঠিক করে নেয়া লেগেছে কোডটা। তারপরও বাগ থেকে যেতো , ইনফিনিটি লুপ অথবা ভুল উত্তর। বাইনারী সার্চ কোড করতে গেলে যে ধরনের বাগে আমরা পড়ি তার জন্য একটা উদাহরন দিয়ে দি আগে:

ধরো তোমার কাছে একটা অ্যারে আছে:

    [1, 1, 3, 3, 4, 4, 4, 4, 5, 9, 20, 20, 21, 21, 21]

এখন তুমি সার্চ করতে চাচ্ছো ৪ এর সর্বোনিম্ন অবস্থানটা, অর্থাৎ 4 নং ইনডেক্স।

তুমি কোড করলা:

    int bug(int Q, int n){
        int lo=0, hi=n, mid;
        while(lo<hi){
            int mid =(lo+hi)/2;
            if(arr[mid]>=Q)
                hi = mid-1;
            else lo = mid+1;
        }
        return mid;
    }

এখানে `Q=4` দিলা। রান করে দেখো কি সব উল্টাপাল্টা উত্তর আসছে! এখন তুমি বসে বসে কোড ঠিক করার চেষ্টা করলে। `while(lo<hi)` হবে নাকি `while(lo<=hi)` হবে? `lo=mid` দিলে কি কাজ হবে? `return` কি `hi/lo/mid` কোনটা করবো?? `hi=mid-1` দেয়ার জন্য কি সমস্যা হচ্ছে? এসব করতে করতে শেষ পর্যন্ত গুগল মামার হেল্প নিলা অথবা বইয়ের স্যুডো কোডটা দেখে ঠিক করে নেয়ার ট্রাই করলা। সচরাচর এমন সমস্যা প্রায় সব কোডারেরই হয়। যাইহোক, এই আর্টিকেলটা লিখতেছি কেবল বাইনারী সার্চের এই অযথা সময় অপচয় দুর করার জন্য। আর্টিকেলটার শেষটুকু পড়ার পর আশা করি তোমাদের বাইনারী সার্চ কোড করার সম্পুর্ন আত্মবিশ্বাস+নির্ভুল কোড করার সামর্থ চলে আসবে।

প্রথমে বলে নি বাইনারী সার্চ দুই ধরনেরই হয়:

* আমরা যে আইটেমটা সার্চ করতে চাই সেটার lowest position টা

নাইলে

* আমরা যে আইটেমটা সার্চ করতে চাই সেটার highest position টা

## Lower Bound Searching

এখানে আমরা চাই অ্যারেতে আইটেমটার সর্বোনিম্ন পজিশনটা খুজে বের করতে। অর্থাৎ `p(f(x))` টা `x` এর সর্বোনিম্ন যে মানের জন্য সত্য হবে। উপরে যে অ্যারেটা দিয়েছিলাম ওটাতে যদি 4 খুজতে চাই তাইলে আমরা 4 নং ইনডেক্সটা রিটার্ন করবে। তোমাদেরকে একটা জিনিষ উপহার দিলাম: `best_so_far`. কোড দেখা শেষ হলে আমাকে মনে মনে গালি দিয়ো না কারন এটা হয়তো অ্যালগরিদমের বইতে দেয়া নাই, সামান্য একটু আপডেট।

    int LowerBound(int Q, int n) {
        int lo=0, hi=n-1;
        int best_so_far=-1;
        while(lo<=hi) {
            int mid = (hi+lo)/2;
            if(arr[mid]>=Q) {
                if(arr[mid]==Q)
                    best_so_far=mid;
                hi = mid-1;
            } else lo = mid+1;
        }
        return best_so_far;
    }

যেহেতু আমরা lower bound খুজে বের করতে চাচ্ছি তাই `arr[mid]>=Q` খুজেছি যেটা আমাদের সর্বনিম্ন ইনডেক্সের দিকে নিয়ে যাবে, আর যদি `arr[mid]==Q` হয় তাইলেই `best_so_far` আপডেট করবো। কোড দেখা শেষ হলে upper bound এর কোডটা দেখে নাও তাইলে সম্পুর্ন ক্লিয়ার হয়ে যাবে ধারনা।

## Upper Bound Searching

এখানে তোমাকে আইটেমটার সর্বোচ্চ পজিশনটা খুজে বের করতে হবে অর্থাৎ `P(f(x)` সত্য হবে সর্বোচ্চ `x` এর যে মানের জন্য। কোডটা দেখো এবার:

    int UpperBound(int Q, int n) {
        int lo=0, hi=n-1;
        int best_so_far=-1;
        while(lo<=hi) {
            int mid = (hi+lo)/2;
            if (arr[mid]<=Q) {
                if(arr[mid]==Q)
                    best_so_far=mid;
                lo=mid+1;
            } else hi=mid-1;
        }
        return best_so_far;
    }

দুইটা কোড কম্পেয়ার করলে বুঝতে পারবে trick টা কেবল `arr[mid]<=Q` এবং `arr[mid]<=Q` তেই আছে জাস্ট `lo=mid+1` `hi=mid-1` এই দুইটার পজিশন চেন্জ করেছি UpperBound ফাংশনে।

হ্যা, বাইনারী সার্চ এতটাই সিম্পল। আশা করি এবার থেকে এটা কোড করতে ঝামেলা হবে না, হইলে লেখক দায়ী নয়। ;)

Keep coding… :)