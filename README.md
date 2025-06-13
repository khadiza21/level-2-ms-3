// video_2 start from here //

> you want to create a sever side with tyscript

# step_1

create a folder and open it with terminal, input the following command
.. npm init -y // for
.. npm i express //
.. npm i -g tyscript // if you not installed globally
.. npm i -D tyscript // only for developer benifit
.. tsc --init // for tyscript configuration

> if you want to deploy this side then create a .gitignore file and create a node_modules folder inside the .gitignor

<!-- module 15 -->
##### Module 15
###### (1) Install MongoDB compass , NoSQl Booster.

###### (3) Insert, insert One, find , findOne, Field filtering, project

- db.test1.find({}).projection({}).sort({ \_id:-1 }).limit(100) ➤ সব ডেটা দেখাবে, শুধু নির্দিষ্ট projection ফিল্ড সহ, আইডি অনুযায়ী উল্টো (নতুন আগে) সাজিয়ে ১০০ টা পর্যন্ত দেখাবে।
- db.test1.findOne({age:17}) ➤ যাদের বয়স ১৭ — এমন প্রথম একটি ডেটা রিটার্ন করবে।
- db.test1.find({gender: "Male"}, {gender: 1}) //field filtering. ➤ শুধু Male জেন্ডার ওয়ালা ডেটাগুলোর gender ফিল্ড দেখাবে।
- db.test1.find({gender: "Male"}, {name:1, email:1, gender: 1}) //field filtering. ➤ Male জেন্ডার ওয়ালা ডেটাগুলোর name, email, gender ফিল্ড দেখাবে।
- db.test1.find({gender:"Male"}).project({name:1, gender:1, email:1}); ➤ Male ডেটাগুলোর নির্দিষ্ট ফিল্ড (name, gender, email) খুঁজে দেখাবে।
  🔸 Note: findOne() এর সঙ্গে .project() ব্যবহার করা যায় না।

###### (4) $eq, $neq , $gt, $lt, $gte, $lte.

- https://www.mongodb.com/docs/manual/reference/operator/query-comparison/
- $eq ➤ সমান মান খুঁজতে
- db.test1.find({age:{$eq:12}}) ➤ বয়স ১২ হলে সে ডেটা দেখাবে
- db.test1.find({gender:{$eq:"male"}}) ➤ জেন্ডার male হলে দেখাবে
- $ne ➤ সমান নয় এমন মান খুঁজতে
- db.test1.find({age:{$ne:12}}) ➤ বয়স ১২ নয় এমন ডেটা দেখাবে
- db.test1.find({gender:{$ne:"male"}}) ➤ male না এমন ডেটা দেখাবে
- $gt ➤ বড় মান খুঁজতে (greater than)
- db.test1.find({age: {$gt:18}}) ➤ বয়স ১৮ এর বেশি হলে দেখাবে which are adult
- db.test1.find({age: {$gt:18}}).sort({age:1}) ➤ বড়দের ডেটা ছোট থেকে বড় বয়স অনুযায়ী সাজিয়ে দেখাবে 1 means sort by ascending.
- $lt ➤ ছোট মান খুঁজতে (less than)
- db.test1.find({age: {$lt:18}}) ➤ বয়স ১৮ এর কম এমনদের দেখাবে
- $gte, $lte ➤ বড় বা সমান / ছোট বা সমান

###### (5) $in , $nin, Implicit and condition

→ অনেকগুলোর মধ্যে যেগুলো আছে/নেই সেগুলোর ওপর ভিত্তি করে ডেটা খোঁজার জন্য। ($in , $nin,)

- $in ➤ নির্দিষ্ট কিছু মানের মধ্যে থাকলে ডেটা দেখাবে
- $nin ➤ নির্দিষ্ট মানগুলোর বাইরে যেগুলো আছে সেগুলো দেখাবে
- Implicit AND ➤ একাধিক শর্ত একসাথে দিলে স্বাভাবিকভাবে AND কাজ করে | {gender:"Female", age: {...}} → gender এবং age দুটো শর্তই মানতে হবে |

- $in : {field:{$in :[value1,value2,.....,value3]}}
- db.test1.find({gender:"Female", age:{$gte:18 , $lte:30}}, {age:1, gender:1}).sort({age:1}); ➤ মেয়েদের মধ্যে যাদের বয়স ১৮ থেকে ৩০ এর মধ্যে, তাদের বয়স ও জেন্ডার ফিল্ড দেখাবে এবং ছোট থেকে বড় বয়স অনুযায়ী সাজাবে।

- db.test1.find({gender:"Female", age:{$in:[18,20,22,24]}}, {age:1, gender:1}).sort({age:1}); //➤ যেসব মেয়েদের বয়স ঠিক ১৮, ২০, ২২, ২৪ — শুধু তাদের ডেটা দেখাবে, সাজানোভাবে। =

- db.test1.find({gender:"Female", age:{$nin:[18,20,22,24]},
interests:{$in:["Cooking","Gaming"]}}, {age:1, gender:1}).sort({age:1}); ➤ যেসব মেয়েদের বয়স ওই নির্দিষ্ট বয়সগুলো না এবং যাদের আগ্রহ Cooking বা Gaming — তাদের বয়স ও জেন্ডারসহ সাজানো ডেটা দেখাবে।

###### (5) $And,$Or, Implict vs Explict

- ✅ $and : {$and:[{expression 1},{expression 2}, {expression 3}.....{expression N}]}
- Explict $and
-  db.test1.find({$and:[{gender:"Female"},{age:{$ne:15}},{age:{$lte:30}}]}).project({age:1, gender:1}).sort({age:1})
- যখন একাধিক শর্ত একসাথে (AND) পূরণ করতে হয় — তখন $and ব্যবহার করা হয়।
এটি এক্সপ্লিসিটলি লেখা যায় অথবা ইম্প্লিসিটলি শুধু কমা দিয়ে শর্ত বসিয়ে।
- 🟢 ব্যাখ্যা: এখানে এমন সকল মেয়ে (Female) ইউজার দেখাবে যাদের বয়স ১৫ নয় এবং ৩০ বা তার কম।


- ✅ $or : {$or:[{expression 1},{expression 2}, {expression 3}.....{expression N}]}
- (Explicit OR condition)
-  db.test1.find({$or:[{gender:"Female"},{age:{$ne:15}},{age:{$lte:30}}]}).project({age:1, gender:1}).sort({age:1})
- 🟢 ব্যাখ্যা: যেসব ইউজার মেয়ে অথবা বয়স ১৫ নয় অথবা বয়স ৩০ বা কম, তাদের দেখাবে।


✅ $or with nested fields
-  db.test1.find({$or:[{"skills.name":"JAVASCRIPT "},{"skills.name":"PYTHON"}]}).project({skills:1}).sort({age:1})
- 🟢 ব্যাখ্যা: যাদের স্কিলের মধ্যে JAVASCRIPT অথবা PYTHON আছে, তাদের skills ফিল্ডসহ দেখাবে।

- ✅ $in : $in (Multiple match check)
- $in ব্যবহার হয় যখন কোনো ফিল্ডের মান একাধিক মানের মধ্যে যেকোনো একটি হলে ম্যাচ করাতে।
- db.test1.find({"skills.name":{ $in : ["JAVASCRIPT","PYTHON"]}}).project({skills:1}).sort({age:1})
🟢 ব্যাখ্যা: যাদের skills.name এর মধ্যে JAVASCRIPT অথবা PYTHON আছে — তাদের skills দেখাবে এবং বয়স অনুযায়ী ছোট থেকে বড় সাজাবে।

* Implicit AND: MongoDB তে যদি একাধিক কন্ডিশন কমা দিয়ে dey, তাহলে এটা অটোমেটিক AND হিসেবে কাজ করে।
* Explicit AND: যদি স্পষ্টভাবে লিখe, তাহলে $and ব্যবহার  kore।