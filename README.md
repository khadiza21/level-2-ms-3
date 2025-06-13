// video_2 start from here //
> you want to create a sever side with tyscript
# step_1
create a folder and open it with terminal, input the following command
.. npm init -y          // for 
.. npm i express        //
.. npm i -g tyscript    // if you not installed globally
.. npm i -D tyscript    // only for developer benifit
.. tsc --init           // for tyscript configuration

> if you want to deploy this side then create a .gitignore file and create a node_modules folder inside the .gitignor


<!-- module 15 -->
####### (1) Install MongoDB compass , NoSQl Booster. 
####### (3) Insert, insert One, find , findOne, Field filtering, project
- db.test1.find({}).projection({}).sort({ _id:-1 }).limit(100)
- db.test1.findOne({age:17})
- db.test.find({gender: "Male"}, {gender: 1}) //field filtering.
- db.test.find({gender: "Male"}, {name:1, email:1,  gender: 1}) //field filtering. 
- db.test1.find({gender:"Male"}).project({name:1, gender:1,  email:1}); // specific filed find kora. findOne er sthe project use kora jay na. 
####### (4) 