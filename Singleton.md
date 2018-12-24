# Singleton
单例模式

## 单例模式的六种写法，各自优缺点
#### 1. 饿汉式
    package com.droid;

    /**
     * 饿汉式单例模式
     * 
     * 缺点：无法对 instance 实例进行延时加载
     * 优化：懒汉式
     * 
     * @author Muran Hu
     *
     */
    public class HungrySingleton {
      private static final HungrySingleton mHungrySingleton = new HungrySingleton();

      private HungrySingleton() {

      }

      public static HungrySingleton getInstance() {
        return mHungrySingleton;
      }
    }
#### 2. 懒汉式
    /**
     * 懒汉式单例模式
     * 
     * 缺点：再多线程并发情况下无法保证实例的唯一性
     * 优化：懒汉线程安全
     * 
     * @author Muran Hu
     *
     */
    public class LazySingleton {
      private static LazySingleton lazySingleton;

      private LazySingleton() {

      }

      public static LazySingleton getInstance() {
        if (null == lazySingleton) {
          lazySingleton = new LazySingleton();
        }

        return lazySingleton;
      }
    }
#### 3. 懒汉线程安全
    /**
     * 线程安全的懒汉模式
     * 
     * 缺点：使用 synchronized 导致性能缺陷
     * 优化：DCL 双重检查锁
     * 
     * @author Muran Hu
     *
     */
    public class LazySafetySingleton {
      private static LazySafetySingleton lazySafetySingleton;

      private LazySafetySingleton() {

      }

      /**
       * 方法中声名synchronized关键字
       * 
       * @return
       */
      public static synchronized LazySafetySingleton getInstance() {
        if (null == lazySafetySingleton) {
          lazySafetySingleton = new LazySafetySingleton();
        }

        return lazySafetySingleton;
      }

      /**
       * 同步代码块实现
       */
      public static LazySafetySingleton getInstance1() {
        synchronized (LazySafetySingleton.class) {
          if (null == lazySafetySingleton) {
            lazySafetySingleton = new LazySafetySingleton();
          }
        }

        return lazySafetySingleton;
      }
    }
#### 4. DCL
    /**
     * 双重检查锁机制
     * 
     * 缺点：JVM 的即时编译器中存在指令重排序的优化
     * 优化：静态内部类 / 枚举
     * 
     * @author Muran Hu
     *
     */
    public class DclSingleton {
      private static DclSingleton dclSingleton;

      private DclSingleton() {

      }

      public static DclSingleton getInstance() {
        // 避免不必要的同步
        if (null == dclSingleton) {
          // 同步
          synchronized (DclSingleton.class) {
            if (null == dclSingleton) {
              dclSingleton = new DclSingleton();
            }
          }
        }

        return dclSingleton;
      }
    }
#### 5. 静态内部类
    /**
     * 静态内部类方式
     * 
     * 优点：JVM 本身机制保证了线程安全，没有性能缺陷
     * 原因：static 、final
     * 
     * @author Muran Hu
     *
     */
    public class StaticInnerSingleton {
      private StaticInnerSingleton() {

      }

      public static StaticInnerSingleton getInstance() {
        return SingletonHolder.mInstance;
      }

      private static class SingletonHolder {
        private static final StaticInnerSingleton mInstance = new StaticInnerSingleton();
      }
    }
#### 6. 枚举
    /**
     * 枚举实现单例
     * 
     * 优点：写法简单，线程安全
     * 
     * @author Muran Hu
     *
     */
    public enum EnumSingleton {
      INSTANCE;
    }
