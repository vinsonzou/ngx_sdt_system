# ngx_sdt_system
使用Nginx 来完成智能的静态容灾系统，帮助在异常时，可以提供静态化的服务做降级和容灾功能。目前已经在折800运行2年多，
为折800的业务抵御了多次意外问题，极大减少事故率。如果对Ngx_Lua开发有兴趣的朋友们，可以购买书籍 << Nginx实战：基于Lua语言的配置、开发与架构详解 >>https://item.jd.com/12487157.html

介绍：
   ngx_sdt_system是采用高性能Ngx_Lua模块开发，可在nginx 和openresty 中方便部署，对业务完全透明化，使用者将可以支持容灾的url（支持精确匹配，正则匹配，还有目录匹配）配置到mysql，
   在配合监控系统（比如nginx_log_analysis的日志分析系统）对url实时监控，当url出现异常后，只需要修改mysql的的字段即可在短时间内将url请求切换到容灾系统。
 
   它拥有如下特性：
   1. 对URL响应异常的服务可以动态切换到容灾系统，支持 比例降级（比如30%的请求分配到容灾系统，剩下的继续访问线上）
   2. 支持服务的智能恢复功能，当请求切换到容灾系统后，容灾系统会镜像用户的请求回线上服务，来验证线上是否恢复，如果线上服务恢复，降级功能会自动解除
   3. 容灾数据的缓存可以以时间版本进行存储，在切换容灾的过程中，可以选择某个时间段的容灾数据，便于切换合适的数据。（如果某个版本没有缓存，就会使用和这个版本最
   的缓存近）
   4. 在不操作mysql切换URL进入容灾系统的情况下，支持偶发性错误降级，对偶发的4xx 5xx可自动重定向到容灾系统获取一份数据提供给客户端，提升用户体验(此功能暂时还没有开发版本出来。)
   5. 如果请求进入容灾系统没有获取到数据，请求支持切换到线上服务重新获取（前提是线上服务仍然可以提供一定的访问能力）

   如果你已经在使用nginx 的日志分析系统：nginx_log_analysis (https://github.com/leehomewl/nginx_log_analysis)，那么静态容灾系统会更方便的使用，  
如果你还没有使用nginx_log_analysis，需要你拥有其他监控工具可以监控 URL的可用性和响应时间，来确认触发容灾。
   如果你任何监控系统都没有，可以使用本系统的 偶发性错误降级功能，配置在mysql 的url可以在后端返回4xx 或者5xx 后，将请求切换到容灾系统的功能，提升用户体验（功能比较单一）
 

安装方式：
  详见https://github.com/leehomewl/ngx_sdt_system/wiki
  
  
