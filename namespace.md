# নেইমস্পেইস

আমাদের ক্লাস, ফাংশন বা কনস্ট্যান্ট নাম নিয়ে প্রায়শই সমস্যায় পড়তে হয় । দেখা যায় আমি যেই নাম ব্যবহার করেছি সেই নামে আরেকটি লাইব্রেরীতে একই নামের কিছু একটা রয়েছে । ফলাফল - নাম নিয়ে কনফ্লিক্ট । এই সমস্যা থেকে সমাধান দিতে পারে নেইমস্পেইস ।

নেইমস্পেইসের ধারনাটা খুবই সাধারন । আমরা যেমন আমাদের ফাইল পত্র গুলো নানা ফোল্ডারে সাজিয়ে রাখি, নেইমস্পেইসও এই ফোল্ডারগুলোর মত । আমাদের ক্লাস, ফাংশন, কনস্ট্যান্ট গুলো আমরা আলাদা আলাদা নেইমস্পেইসে সাজিয়ে রাখি । এতে এক নেইমস্পেইসের সাথে আরেক নেইমস্পেইসের জিনিসপত্রের নাম নিয়ে কোন কনফ্লিক্ট হয় না ।

এর আগে এই ধরনের নাম সংক্রান্ত জটিলতা এড়াতে ডেভেলপাররা আন্ডারস্কোর ব্যবহার করে নেইমস্পেস এর কাজ চালাতো । পুরোনো ফ্রেমওয়ার্কগুলোত এই ধরনের আন্ডারস্কোর বেইজড নেইমস্পেসিং এর প্রচেষ্টা দেখা যায় । পিএইপি ৫.৩ থেকে নেইমস্পেইস ল্যাঙ্গুয়েজ ফিচার হিসেবে যোগ করা হয় ।

## নেইমস্পেইস তৈরি করা

নেইমস্পেইসের ভিতরে যে কোন ভ্যালিড পিএইচপি কোডই রাখা যায় । তবে নেইমস্পেইসের প্রকৃত ইফেক্ট পড়ে শুধুমাত্র ক্লাস, ইন্টারফেইস, কন্সট্যান্ট এবং ফাংশনের উপর । অর্থাৎ এগুলোকেই শুধু নেইমস্পেইসে আটকানো যায় ।

আমাদের নেইমস্পেইস ডিফাইন করতে প্রথমে `namespace` কিওয়ার্ড এবং তারপর নেইমস্পেইস এর নাম দিতে হয় । নেইমস্পেইস ডিক্লেয়ার করা শুরু হতে হবে পিএইচপি ফাইলের একেবারে উপর থেকে অর্থাৎ অন্য যে কোন কোডের আগে । একমাত্র বিকল্প শুধু `declare` কিওয়ার্ডটি, এটিই শুধু নেইমস্পেস ডিক্লেয়ারেশনের আগে আসতে পারে । একই ফাইলে একাধিক নেইমস্পেইস ডিক্লেয়ার করা সম্ভব । পরবর্তী নেইমস্পেইস এর আগ পর্যন্ত সব কোডই প্রথম নেইমস্পেইস এর অন্তর্গত ।

উদাহরণ:

```php
<?php
namespace MyProject\SubNameSpace\AnotherLevel;

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }

?>
```

আমরা চাইলে নেইমস্পেইস এর পর কার্লি ব্রেইস \(সেকেন্ড ব্রাকেট\) ব্যবহার করেও নেইমস্পেইসগুলোকে আলাদা করতে পারি । নেইমস্পেইসের নাম দেওয়া না হলে সেটি গ্লোবাল নেইমস্পেইস হিসেবে বিবেচ্য হয় । অর্থাৎ নামহীন নেইমস্পেইসে আমরা যাই ডিফাইন করি তা গ্লোবাল নেইমস্পেইস থেকেই এ্যাক্সেস করা যায় ।

## নেইমস্পেইস ব্যবহার করা

প্রথমেই নিশ্চিত হতে হবে আমাদের কোড যে নেইমস্পেইসে আছে তা বর্তমান ফাইল থেকে এ্যাক্সেস করা যায় কিনা । যেমন: যদি নেইমস্পেইসটি অন্য কোন ফাইলে হয় তবে অবশ্যই সেটি ইনক্লুড করে নিতে হবে । তবে বাস্তবে বেশীরভাগ ক্ষেত্রেই আমরা অটোলোডার ব্যবহার করে নেইমস্পেইস থেকে কোড ইম্পোর্ট করতে পারবো । সেক্ষেত্রে ম্যানুয়ালি ইনক্লুড করা লাগবে না ।

এরপর আমরা `use` কিওয়ার্ডটি ব্যবহার করে তারপর নেইমস্পেইস সহ পুরো নাম উল্লেখ করবো । উদাহরণ:

```php
<?php 
require 'db.php'; 

use MyProject\DB; 
use MyProject\DB\Connection as DBC; 

$x = new DBC(); 

?>
```

এই উদাহরনে আমরা দেখছি কিভাবে কোন নেইমস্পেইস থেকে আমরা ক্লাস ইম্পোর্ট করলাম । `as` কিওয়ার্ডটি ব্যবহার করে আমরা ইম্পোর্ট করার সময় প্রয়োজনমত নাম পরিবর্তন করে দিতে পারি ।

## নেইমস্পেইস থেকে গ্লোবাল কোড এ্যাক্সেস করা

আমরা কোন নেইমস্পেইস থেকে যদি কোন ক্লাস বা ফাংশন এর পুরো নেইমস্পেইসড নাম ব্যবহার না করে শুধু নাম উল্লেখ করি তাহলে পিএইচপি ধরে নেয় ঐ ক্লাস বা ফাংশনও একই নেইমস্পেইসেরই অংশ । যেমন আমরা যদি `MyProject` নেইমস্পেইসে থেকে `strlen` ফাংশনটি কল করি তাহলে পিএইচপি গ্লোবাল `strlen()` ফাংশনটি ব্যবহার না করে `MyProject\strlen()` ফাংশনটি খুজঁবে । তাই কোন নেইমস্পেইসের ভিতর থেকে গ্লোবাল নেইমস্পেইসের ক্লাস, ফাংশন ইত্যাদি এ্যাক্সেস করার সময় নামের শুরুতে একটি `\` ব্যবহার করতে হয় । যেমন:

```php
<?php
namespace Foo;
$a = \strlen('hi');
```

