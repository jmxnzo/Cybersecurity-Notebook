alert http $EXTERNAL_NET any -> $HTTP_SERVERS any (msg:"ET WEB_SERVER Possible SQL Injection Attempt SELECT FROM"; flow:established,to_server; content:"SELECT"; nocase; http_uri; content:"FROM"; nocase; http_uri; pcre:"/SELECT\b.*FROM/Ui"; reference:url,en.wikipedia.org/wiki/SQL_injection; reference:url,doc.emergingthreats.net/2006445; classtype:web-application-attack; sid:2006445; rev:13;)

alert http $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"ET WEB_SERVER Possible SQL Injection Attempt UNION SELECT"; flow:established,to_server; uricontent:"UNION"; nocase; uricontent:"SELECT"; nocase; pcre:"/UNION.+SELECT/Ui"; reference:url,en.wikipedia.org/wiki/SQL_injection; reference:url,doc.emergingthreats.net/2006446; classtype:web-application-attack; sid:2006446; rev:11;)

alert http $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"ET WEB_SERVER MYSQL SELECT CONCAT SQL Injection Attempt"; flow:established,to_server; uricontent:"SELECT"; nocase; uricontent:"CONCAT"; nocase; pcre:"/SELECT.+CONCAT/Ui"; reference:url,ferruh.mavituna.com/sql-injection-cheatsheet-oku/; reference:url,www.webdevelopersnotes.com/tutorials/sql/a_little_more_on_the_mysql_select_statement.php3; reference:url,doc.emergingthreats.net/2011042; classtype:web-application-attack; sid:2011042; rev:3;)


alert udp any 53 -> any $HOME_NET (msg:"ET DNS Excessive DNS Responses with 1 or more RR's (100+ in 10 seconds) - possible Cache Poisoning Attempt"; threshold: type both, track by_src, count 100, seconds 10;  sid:200; rev:1;)
