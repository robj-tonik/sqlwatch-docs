# Time zone changes

Currently changing the time zone to an earlier time or switching from summer to winter time is not supported. This is because we're storing local timestamps and not UTC dates and means, that when we set the clock backward by 1 hour it will start recording snapshots with the same timestamp it had already recorded which will violate primary key. This will only last 1 hour after which it should stop failing and will carry on as usual.

If we change the time zone to let’s say -6 hours, it will be failing for another 6 hours until it starts recording new snapshots \(with a timestamp that does not already exists\)

The fix would be to use time zone agnostic UTC formatted dates across SQLWATCH tables.

