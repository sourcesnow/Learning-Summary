#1，使用session_status()来判断是否启动session
***session_status()!=PHP_SESSION_ACTIVE***
#2，session通过cookie的方式分配phpsessid，可以通过chrome的DevTools查看network，获得当前session的id

*例如*
*session.php*
<?php 
  session_start();
  sleep(5);
  var_dump($_SESSION);
 ?>
 *session1.php*
 <?php 
  session_start();
  var_dump($_SESSION);
 ?>
 *同一个browser中开启两个tab同时运行两个script，会发现只有第一个运行完，才能运行运行第二个，但两个browser打开，就不会有这样的现象，因为php关于的session的处理方式使用的是
 file方式，导致同一个browser访问时，第一个运行时，会被服务器识别session_id ,会相应的启动文件锁，锁定相应的id对应的文件，故同一个browser同时访问，则需要等待，第一个使用完结，但可以使用session_write_close()可以关闭正在使用的文件锁，但需要重新进行session_start()*
#4，可以通过setcoookie()函数，服务器可以向客户端发送cookie，设置session的expired时间，时间是以秒为单位
#5，sessoin的销毁可以通过session_destory()函数进行，这个函数是彻底销毁了session的文件，类似于关闭浏览器。同时自带有GC模式的清理方式，通过gc_probability/gc_divisor，及在gc_divisor次请求中，可能触发gc_probability次gc清理。