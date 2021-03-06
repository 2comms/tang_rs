(Jun 11, 2020)
----------------------
### Add
- Enable `Pool<Manager>::clear` and `Pool<Manager>::pause` for single threaded pool.
- `Pool<Manager>::thread_id` would return the `ThreadId` the single threaded pool runs on.

(Jun 2, 2020)
----------------------
### Breaking
- `Builder::build_uninitialized` return `Pool<Manager>` directly and no unwrap needed.


(Jun 1, 2020)
----------------------
### Breaking
- `Manager` trait use concrete type `ManagerTimeout` for Timeout. This helps to reduce one `Box` every time we try to get a connection.


(May 28, 2020)
----------------------
### Breaking
- `Pool::run` would pass `PoolRef` to closure. This way the async block doesn't have to be wrapped by `Box::pin` therefore reduce allocation.


(May 27, 2020)
----------------------
### Add
- export `PoolRefOwned` type.


(May 25, 2020)
----------------------
### Add
- `Pool<Manager>::get_owned` to get a connection without any direct reference which can be moved to async blocks and across any await point.
- `no-send` feature introduce a single threaded pool which have considerable more performance than multi threaded pool. Usage showed in `ntex_example`


(May 13, 2020)
----------------------
### Add
- `Pool<Manager>::clear` to clear the pool.
  

(May 12, 2020)
----------------------
### Add
- `Pool<Manager>::set_max_size` to change the max size of pool on the fly.
  

(May 11, 2020)
----------------------
### Add
- `Pool<Manager>::pause` and `Pool<Manager>::resume` methods to pause and restart the pool.
  

(May 9, 2020)
----------------------
### Breaking
- `Manager` trait: Remove `schedule_inner` and `garbage_collect_inner`. `on_start` do nothing by default.
- This make the trait more simple to impl for non scheduled cases.
### Add
- `Manager::on_stop` method which will be called when `Pool<Manager>` is dropping.
- `ScheduleReaping`, `GarbageCollect` and `ManagerInterval` trait for scheduled work.(See basic_example for usage)


(April 28, 2020)
----------------------
### Breaking
- Remove all 3rd party deps and only rely on std
- `Manager` trait have to handle all the implementation related to async runtime.
### Add  
- Can run on any async runtime.  


(April 26, 2020)
----------------------
### Add
- Expose `Manager` with `Pool<Manager>::get_manager`


(April 25, 2020)
----------------------
### Breaking
- Split into multiple crate


(April 9, 2020)
----------------------
- Update dependencies


(October 29, 2019)
----------------------
### Breaking
- default feature now doesn't include `tokio-postgres` and `redis` anymore. examples have been updated according to this change


(October 24, 2019)
----------------------
### Add
- `Builder::build_uninitialized` for building an empty `Pool<Manager>` that can be initialized manually with `Pool<Manager>::init` method.
This enable use of `Pool<Manager>` with `lazy_static`.


(October 16, 2019)
----------------------
### Add
- `tang_rs::PrepareStatement` for add/remove prepared statements(Statements that constructed when a connection spawn) to `PoolRef<PostgresManager<_>>`


(October 14, 2019)
----------------------
### Add
- `tang_rs::CacheStatement` for bulk insert/remove statements to `PoolRef<PostgresManager<_>>`


(October 11, 2019)
----------------------
### Breaking
- `PostgresManager` use `prepare_statement` method to accept prepared statement when building manager.
- `PoolRef` gives a `HashMap<String, Statement>` instead of `Vec<Statement>`. 
- examples have been updated according to these changes.


(October 3, 2019)
----------------------
### Breaking
- Return error type `tang_rs::PostgresPoolError` and `tang_rs::RedisPoolError` when use `Pool<Manager>.get()`
### Add
- `PoolRef.take_conn()` method to take the ownership of connection out from pool.
- `Builder.queue_timeout(<Duration>)` method to indicate the timeout of waiting queue for pool.