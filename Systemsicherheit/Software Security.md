
Input validation: 
- the root of much evil
- properly validate data at the entry and exit points of the application
- can significantly reduce the impact of attacks if implemented properly: injection of malicious input, such as code, scripting, commands, that can be interpreted/executed by different targets to exploit vulnerabilities
- Impact: Phishing, information disclosure, data modification, DoS, financial/reputation loss, fraud

Different strategies of validation:
	- syntactic validation: enforces correct syntax of structured fields(e.g. SSN, date)
	-  semantic validation enforces correctness of their values in a specific context (e.g. start date is before end date)

### Whitelisting
- Check that user-provided input is in some set of values known to be safe
- fixing invalid inputs may introduce new vulnerabilities
Whitelisting is usually done via Regex, depending on how you define the regular expression(s), even "O'Brian" would be allowed. Whitelisting ensures that we know which inputs (especially which "dangerous" characters) can be used. Since we now know that the input may contain a ', we would first escape it before passing it to the query.
Whitelists have to be specific, and not general.

### Blacklisting
Problems
- problem if we blacklist all special characters, may conflict with the functionality(blacklisting validate inputs too, like the name O'Brian)
- How do you know if/when you’ve eliminated all possible ‘bad’ strings?


## Regex
^ matches position just before the first character of the string
$ matches position just after the last character of the string
? match zero or one instance of this character.
regex Great!? will match Great or Great!.
- beware - take exponential time and memory to process certain data (ReDoS)

Sql injection: 
- Input examples:
	- 0‘ OR 1=1 -- (')
	- 0' AND 1=0 UNION SELECT cardholder, number, exp_date FROM creditcards --(')
	- ' ; DROP TABLE creditcards --(')
	- ' ;INSERT INTO admin VALUES (‘hacker’, ...) --(')
- because comments are quoated, we need to circumvent the quotes with commenting
	- abc’ ;DROP TABLE creditcards ; -- (')
- SQL comment --

### Client-side validation is NOT enough
•Client/Server system: all input validations should be performed at the server
– Validation only makes sense when executed in a correct environment
– Client can be controlled by the attacker
• Attacker can subvert client or write their own!
### Why do we bother validating at clients then?
– Input validation at client-side can improve user response & lower server load
– BUT, all input validations performed by the client must be redone by the server!


### Prepared statements: 
- allow creation of queries with bind variables
- Parameters not involved in query parsing
- Structure of the intended query is preserved