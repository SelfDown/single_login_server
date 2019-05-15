# single_login_server
场景：服务器A，访问服务器B数据服务。服务器B 需要登录验证，根据不同的用户登录，获取不同的信息，比如用户ID，需要不同sessionid表标志。B服务器

解决办法，当A服务器验证后，在session 里保存，B服务器的sessionID_From_B。

当用户请求A服务器数据，A请求B服务器数据，发现没有登录（sessionID_From_B,为空），直接登录一次，记录sessionID
当用户请求A服务器数据，A请求B服务器数据，有sessionID_From_B，直接请求数据，放回结果为过期，直接登录一次，更新数据
当用户请求A服务器数据，A请求B服务器数据，有sessionID_From_B，直接请求数据，有结果，直接返回


