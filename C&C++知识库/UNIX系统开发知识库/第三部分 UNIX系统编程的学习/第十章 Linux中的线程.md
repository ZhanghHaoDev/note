# 线程的概念

- **线程**：轻量级进程（LWP），共享进程的地址空间但拥有独立的执行栈和寄存器。
- **进程**：拥有独立的地址空间和PCB（进程控制块）。
- **Linux线程**：在Linux下，线程是最小的执行单位，进程是最小的资源分配单位。

# 线程控制源语

## 线程ID函数
- **`pthread_self`**：获取当前线程的ID。

## 创建子线程
- **`pthread_create`**：创建新线程。
  ```c
  int pthread_create(pthread_t *tid, const pthread_attr_t *attr, void *(*start_routine)(void *), void *arg);
  ```

## 线程退出
- **`pthread_exit`**：退出当前线程。
  ```c
  void pthread_exit(void *retval);
  ```

## 回收线程
- **`pthread_join`**：等待线程结束并回收资源。
  ```c
  int pthread_join(pthread_t thread, void **retval);
  ```

## 取消线程
- **`pthread_cancel`**：请求取消其他线程。
  ```c
  int pthread_cancel(pthread_t thread);
  ```

## 分离线程
- **`pthread_detach`**：设置线程为分离状态，线程结束后自动回收资源。
  ```c
  int pthread_detach(pthread_t thread);
  ```

# 线程同步

## 互斥锁（Mutex）
- **`pthread_mutex_t`**：定义互斥锁。
- **`pthread_mutex_init`**：初始化互斥锁。
- **`pthread_mutex_lock`**：加锁。
- **`pthread_mutex_unlock`**：解锁。
- **`pthread_mutex_destroy`**：销毁互斥锁。

## 读写锁（RWLock）
- **`pthread_rwlock_t`**：定义读写锁。
- **`pthread_rwlock_init`**：初始化读写锁。
- **`pthread_rwlock_rdlock`**：以读模式加锁。
- **`pthread_rwlock_wrlock`**：以写模式加锁。
- **`pthread_rwlock_unlock`**：解锁。
- **`pthread_rwlock_destroy`**：销毁读写锁。

## 条件变量
- **`pthread_cond_t`**：定义条件变量。
- **`pthread_cond_init`**：初始化条件变量。
- **`pthread_cond_wait`**：等待条件变量。

# 线程使用注意事项

- 确保线程结束后资源被正确回收。
- 避免在线程中使用不安全的库函数。
- 调试多线程程序可能比较困难。

# 线程同步的重要性

- 避免数据混乱和竞争条件。
- 确保数据一致性。

# 死锁

- 避免不当使用锁导致死锁。

# 补充知识

- **`pthread_attr_t`**：线程属性对象，用于控制线程的创建和行为。
- **`pthread_key_t`**：线程局部存储，用于在线程之间共享数据。
