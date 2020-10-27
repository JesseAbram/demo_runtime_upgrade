# Runtime Upgrade Demo Testing

## Setup
* build all three branches (master, good_upgrade, and bad_upgrade)
* I recommend renaming the target folders to something like (targetNormal, targetGood, targetBad) (this will avoid having to recompile)
* run your normal blockchain then forkit
### first Halva test
* The tests are suppose to allow you to use one test and rerun it multiple times to show how it reacts to properly and unproperly migrated state
* To set it up (give your chain an initial state) you need to run the test once 
* navigate to halva
* yarn install 
* yarn test
### forkit
* cd forkit
* npm install
* copy paste your binary (rename it binary) and your runtime for the desiered chain into the data folder 
* npm start
* stop your normal blockchain and run this one ./data/binary --chain data/fork.json --alice 
* make sure to purge chain after finishing
### Second Halva test
* just run yarn test 

When running against a properly migrated chain you should get 
 ```
Halva test
    Runtime Upgrade
{ somethingFirst: { sth_else: true, something: '12' } }
already upgraded blockchain
{ something: { sth_else: true, something: '12' } }
{ somethingAfter: { sth_else: true, something: '12' } }
      ✓ wasm upgrade
```

When running against the improperly upgraded test you should get 
```
 Halva test
       Runtime Upgrade
         wasm upgrade:

      AssertionError: expected { sth_else: false, something: '0' } to deeply equal { something: '12', sth_else: true }
      + expected - actual

       {
      -  "something": "0"
      -  "sth_else": false
      +  "something": "12"
      +  "sth_else": true
       }
```
