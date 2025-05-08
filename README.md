# Blog Post-1:<br/>
## TypeScript-এ interface এবং type এর মধ্যে কী কী পার্থক্য রয়েছে? <br/>
TypeScript ব্যবহারের অন্যতম বড় সুবিধা হচ্ছে টাইপ সিস্টেম। আর এই টাইপ সিস্টেমের দুটো গুরুত্বপূর্ণ অংশ হলো interface এবং type। অনেকেই সমস্যায় পড়ে যান—কখন interface ব্যবহার করব, আর কখন type? এই ব্লগ পোস্টে আমরা সহজ ও বিস্তারিতভাবে জানতে পারব ইনশা-আল্লাহ: <br/>
ছোট করে জেনে নেই আমরা কি বিষয়ে জানতে পারব? <br/>
 interface ও type কি? <br/>

 এদের মধ্যে পার্থক্য কী? <br/>

 কখন কোনটা ব্যবহার করা ভালো? <br/>

 উদাহরণসহ দেখতে পারব। <br/>
<br/>

## interface এবং type কী? <br/>

interface:<br/>
interface মূলত একটি অবজেক্টের স্ট্রাকচার বা গঠন বর্ণনা করতে ব্যবহৃত হয়। এটা একধরনের চুক্তি (contract)—যেখানে আপনি বলবেন, এই অবজেক্টে এই এই প্রপার্টিগুলো থাকবে।<br/>
<br/>
interface User {
  name: string;
  age: number;
}
<br/>
type: <br/>
type অনেক বেশি ফ্লেক্সিবল। আপনি শুধু অবজেক্ট নয়, ইউনিয়ন টাইপ, টুপল, ফাংশন সিগনেচার, প্রিমিটিভ টাইপ ইত্যাদিও নির্ধারণ করতে পারবেন। <br/>
<br/>
type User = {
  name: string;
  age: number;
}
<br/>
type ID = string | number;<br/>

## interface বনাম type: মূল পার্থক্য-<br/>
Extending/Inheritance          :interface সহজভাবে extends দিয়ে বর্ধিত করা যায়, যেমন: interface Admin extends User {}। অন্যদিকে type-এ এক্সটেনশন করতে হলে & (intersection) অপারেটর ব্যবহার করতে হয়, যেমন: type Admin = User & { role: string }। <br/>
Declaration Merging            :interface একই নামে একাধিকবার ঘোষণা করলে তারা একত্রিত (merge) হয়ে যায়। এটা API বা লাইব্রেরি এক্সটেনশনের জন্য বেশ উপযোগী। অন্যদিকে type-এ একই নামের একাধিক ডিক্লারেশন করা যায় না; করলে টাইপ এরর হয়। <br/>
Use Cases                      :interface সাধারণত অবজেক্ট ও ক্লাসের স্ট্রাকচার বর্ণনার জন্য উপযুক্ত। পক্ষান্তরে type অনেক বেশি ফ্লেক্সিবল—এটা ফাংশন টাইপ, টুপল, ইউনিয়ন, ইন্টারসেকশন ইত্যাদি নানা ধরনের টাইপ সংজ্ঞায়িত করতে পারে। <br/>
Performance (compilation time) :কম্পাইল টাইমে interface তুলনামূলকভাবে একটু দ্রুত কাজ করে। যদিও এই পার্থক্য সাধারণত খুব সামান্য, বড় প্রজেক্টে এটি প্রভাব ফেলতে পারে। অন্যদিকে type কিছুটা ধীর হতে পারে, বিশেষ করে যখন অনেক বেশি জটিল টাইপ সংমিশ্রণ থাকে। <br/>
<br/>
<br/>

### কখন interface ব্যবহার করবেন? <br/>
যখন আপনি একটি অবজেক্ট বা ক্লাসের স্ট্রাকচার বর্ণনা করছেন। <br/>

যখন ভবিষ্যতে টাইপটি একাধিক জায়গায় বাড়ানো লাগতে পারে।<br/>

যখন আপনি চাইছেন টাইপ মার্জিং বা ডিক্লারেশন মার্জিং হোক।<br/>

উদাহরণ: <br/>
interface Person {
  name: string;
  age: number;
}
<br/>
interface Person {
  email: string;
}
<br/>
const p: Person = {
  name: "Shawon",
  age: 25,
  email: "shawon@example.com"
};
<br/>
### কখন type ব্যবহার করবেন?<br/>
যখন আপনাকে ইউনিয়ন টাইপ, টুপল, অথবা ফাংশন টাইপ ডিফাইন করতে হবে।<br/>

যখন টাইপে প্রিমিটিভ বা কাস্টম টাইপ একত্রে ব্যবহারের দরকার হয়।<br/>

যখন জটিল টাইপ কম্বিনেশন দরকার হয়।<br/>

উদাহরণ: <br/>
<br/>
type ID = number | string;
<br/>
type User = {
  id: ID;
  name: string;
};
<br/>
type Admin = User & {
  role: "admin";
};
<br/>
## বাস্তব উদাহরণ: <br/>
### interface দিয়ে অবজেক্ট স্ট্রাকচার: <br/>
<br/>
interface Car {
  brand: string;
  speed: number;
  drive(): void;
}
<br/>
const myCar: Car = {
  brand: "Toyota",
  speed: 120,
  drive() {
    console.log("Driving fast!");
  }
};
<br/>
###  type দিয়ে ফাংশন ও ইউনিয়ন টাইপ:<br/>
<br/>
type Add = (a: number, b: number) => number;

const sum: Add = (a, b) => a + b;

type Shape = "circle" | "square" | "triangle";

## মনে রাখার টিপস: <br/>

যদি আপনি শুধু অবজেক্ট টাইপ ব্যবহার করছেন—interface বেছে নিন। <br/>

যদি টাইপের ফর্ম অনেক বেশি জটিল হয়—type বেছে নিন। <br/>

যদি চান ফিউচারে টাইপটা সহজে এক্সটেন্ড করতে—interface ভালো পছন্দ। <br/>

যদি ফাংশন টাইপ বা ইউনিয়ন টাইপ দরকার হয়—type ভালো কাজ করবে।<br/>
<br/>
## উপসংহার: <br/>
interface আর type দুটোই TypeScript-এ টাইপ ডিফাইন করার শক্তিশালী উপায়। আপনি কোনটা ব্যবহার করবেন সেটা নির্ভর করে আপনার প্রয়োজন এবং কনটেক্সটের উপর।
সর্বোত্তম অভ্যাস হচ্ছে—যেখানে সম্ভব interface ব্যবহার করুন, এবং যেখানে interface সীমাবদ্ধ, সেখানেই type ব্যবহার করুন।<br/>
<br/>
BLOG POST-2:<br/>
