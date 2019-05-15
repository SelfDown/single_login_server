# single_login_server
场景：服务器A，访问服务器B数据服务。服务器B 需要登录验证，根据不同的用户登录，获取不同的信息，比如用户ID，需要不同sessionid表标志。B服务器

原理：当用户访问服务器，服务器会从当前请求中cookies 中去sessionId 字段（每个请求都会带），如果没有sessionId,直接返回未登录。如果有sessionId,服务器验证是否过期、正确，通过则返回数据，否则返回未登录。所以请求关键因素就是sessionId,服务器认为你有没有登录，就靠sessionId.

解决办法，当A服务器验证后，在session里保存，B服务器的sessionId,字段为sessionID_From_B。


当用户请求A服务器数据，A请求B服务器数据，发现没有登录（sessionID_From_B,为空），直接登录一次，记录sessionID


当用户请求A服务器数据，A请求B服务器数据，有sessionID_From_B，直接请求数据，放回结果为过期，直接登录一次，更新数据


当用户请求A服务器数据，A请求B服务器数据，有sessionID_From_B，直接请求数据，有结果，直接返回


