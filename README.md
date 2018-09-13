Original `GFQuery` call back returns `GFEventType` and `CLLocation` but with these `GFQuery` classes you can have `FIRDataSnapshot` as well in same call back.

**Original callback:**
   
    [query observeEventType:GFEventTypeKeyEntered withBlock:^(NSString *key, CLLocation *location) {
          // NSLog(@"Key '%@' entered the search area and is at location '%@'", key, location);
    }];
    
**With these classes:**
   
    [query observeEventType:GFEventTypeKeyEntered withBlock:^(NSString *key, CLLocation *location, FIRDataSnapshot *snapshot) {
          // NSLog(@"Key '%@' entered the search area and is at location '%@'", key, location);
          NSLog(@"%@", snapshot.value);
    }];


Also there is one more call back `onChangeBlock` to identify the change in any node with in the location radius provided to `GFQuery`.
Observe it after `readyBlock`, See below example:

    [query observeReadyWithBlock:^{
        NSLog(@"Ready");
        /// Add your onChangeBlock here
        query.onChangeBlock = ^(FIRDataSnapshot * _Nonnull snapshot, FIRDataEventType eventType) {
            NSLog(@"%@", snapshot.value);
        };
    }];
    
**Installations:**
Just replace these files with existing `GFQuery.h` & `GFQuery.m` files.
