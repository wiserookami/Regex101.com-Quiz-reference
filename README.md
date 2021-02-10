# Regex101.com-Quiz-reference #

- 链接[https://regex101.com/quiz](https://regex101.com/quiz "https://regex101.com/quiz")

## 描述 ##

	其中的代码指的是正则表达式的Python代码实现。
	参考的一部分是粘贴来的，能优化的就优化了一下，一部分是自己写的，有些写的很勉强。但无论哪种都仅供参考，为没有思路的你提供一点思路，也请努力思考后再去翻看。
	如果你想要更详细的解释，推荐在stackoverflow -> https://stackoverflow.com/里面直接搜索题目，希望你可以找到自己想要的。
	在很多问题上，我们可以依靠使用的编程语言，并不是非要一个正则表达式来解决所有问题，而且只使用一个正则表达式不代表它的效率就高，所以不要纠结，灵活变通才是解决问题之本。
	实现思路一但固定，再去想其他的实现思路就会变的很困难，如果你有其他的实现思路，无论好坏，请务必告诉我。

## 目录 ##

- [Task 1: Word Boundaries](#task-1-word-boundaries)
- [Task 2: Capitalizing I](#task-2-capitalizing-i)
- [Task 3: Uppercase Consonants](#task-3-uppercase-consonants)
- [Task 4: Retrieve Numbers](#task-4-retrieve-numbers)
- [Task 5: Whitespace](#task-5-whitespace)
- [Task 6: Broken Keyboard](#task-6-broken-keyboard)
- [Task 7: Validate an IP](#task-7-validate-an-ip)
- [Task 8: HTML Tags](#task-8-html-tags)
- [Task 9: Match an E-Mail](#task-9-match-an-e-mail)
- [Task 10: Followed by](#task-10-followed-by)
- [Task 11: Validate Floating Point Numbers](#task-11-validate-floating-point-numbers)
- [Task 12: Match any number between 0-100](#task-12-match-any-number-between-0-100)
- [Task 13: Match alternating 0s and 1s in any order](#task-13-match-alternating-0s-and-1s-in-any-order)
- [Task 14: Spam Filter](#task-14-spam-filter)
- [Task 15: Not Surrounded By Digits](#task-15-not-surrounded-by-digits)
- [Task 16: Repeated Words](#task-16-repeated-words)
- [Task 17: Start before End](#task-17-start-before-end)
- [Task 18: Every other digit](#task-18-every-other-digit)
- [Task 19: The Thousands](#task-19-the-thousands)
- [Task 20: Quoted Text With Escapes](#task-20-quoted-text-with-escapes)
- [Task 21: Replace Text, Not Code](#task-21-replace-text-not-code)

## Task 1: Word Boundaries ##

	Check if a string contains the word word in it (case insensitive). If you have no idea, I guess you could try /word/.

	参考: /\bword\b/g
	代码: re.findall(r"\bword\b", "...", re.I | re.S)

## Task 2: Capitalizing I ##

	Use substitution to replace every occurrence of the word i with the word I (uppercase, I as in me). E.g.: i'm replacing it. am i not? -> I'm replacing it. am I not?. A regex match is replaced with the text in the Substitution field when using substitution.

	参考: s/\bi\b/I/g
	代码: re.sub(r"\bi\b", r"I", "...", flags=re.S)

## Task 3: Uppercase Consonants ##

	With regex you can count the number of matches. Can you make it return the number of uppercase consonants (B,C,D,F,..,X,Y,Z) in a given string? E.g.: it should return 3 with the text ABcDeFO!. Note: Only ASCII. We consider Y to be a consonant! Example: the regex /./g will return 3 when run against the string abc.

	参考: /[^AEIOUa-z_\d\W]/g
	参考: /(?=[B-Z])[^EIOU]/g
	参考: /(?![EIOU])[B-Z]/g
	代码: re.findall(r"(?=[B-Z])[^EIOU]", "...", re.S)

## Task 4: Retrieve Numbers ##

	Count the number of integers in a given string. Integers are, for example: 1, 2, 65, 2579, etc.

	参考: /\d+/g
	代码: re.findall(r"\d+", "...", re.S)

## Task 5: Whitespace ##

	Find all occurrences of 4 or more whitespace characters in a row throughout the string.

	参考: /\s{4,}/g
	代码: re.findall(r"\s{4,}", "...", re.S)

## Task 6: Broken Keyboard ##

	Oh no! It seems my friends spilled beer all over my keyboard last night and my keys are super sticky now. Some of the time whennn I press a key, I get two duplicates. Can you ppplease help me fix thhhis?

	参考: /(.)\1\1/g
	参考: /(.)\1{2}/g
	代码: re.findall(r"(?P<T1>.)(?P=T1)(?P=T1)", "...", re.S)

## Task 7: Validate an IP ##

	Validate an IPv4 address. The addresses are four numbered separated by three dots, and can only have a maximum value of 255 in either octet. Start by trying to validate 172.16.254.1.

	参考: /^(?:(?:\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.){3}(?:\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])$/g
	参考: /^(?:(?:25[0-5]|2[0-4]\d|1\d\d|[1-9]\d|\d)(?:\.(?!$)|$)){4}$/g
	参考: /^(?:(?:\d|1\d{1,2}|[2-9]\d|2[0-4]\d|25[0-5])(?:\.(?!$)|$)){4}$/g
	参考: /^(?:(?:25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)(?:\.(?!$)|$)){4}$/g
	参考: /^(?:(?:25[0-5]|2[0-4]\d|[01]?\d?\d)(?:\.(?!$)|$)){4}$/g
	代码: re.findall(r"^(?:(?:25[0-5]|2[0-4]\d|[01]?\d?\d)(?:\.(?!$)|$)){4}$", "...", re.S)

## Task 8: HTML Tags ##

	Strip all HTML tags from a string. HTML tags are enclosed in < and >. The regex will be applied on a line-by-line basis, meaning partial tags will need to be handled by the regex. Don't worry about opening or closing tags; we just want to get rid of them all. Note: This task is meant to be a learning exercise, and not necessarily the best way to parse HTML.

	参考: s/<[^>]*|[^<]*>//g
	代码: re.sub(r"<[^>]*|[^<]*>", "", "...", flags=re.S)

## Task 9: Match an E-Mail ##

	Verify that a given e-mail address is valid. We all know how complex emails are, but despite this, let's give it a try and see what we can come up with. You could start by trying to match contact@regex101.com (denoted as <local-part>@<domain>.<top-level-domain>).

	参考: /^[^\.\s@()<>,;:\\\"\[\]]+\.?[^\.\s@()<>,;:\\"\[\]]+@([a-zA-Z][a-zA-Z\d-]*?(?<!-)\.)+[a-zA-Z]{2,6}$/g
	参考: /^(?:[^\.\s@()<>,;:\\\"\[\]]+\.?){2}(?<!\.)@(?:[a-zA-Z][a-zA-Z\d-]*?(?<!-)\.)+[a-zA-Z]{2,6}$/g
	代码: re.findall(r"^(?:[^\.\s@()<>,;:\\\"\[\]]+\.?){2}(?<!\.)@(?:[a-zA-Z][a-zA-Z\d-]*?(?<!-)\.)+[a-zA-Z]{2,6}$", "...", re.S)

## Task 10: Followed by ##

	For every occurence of the char #, match the previous character and save it in a group (backreference). Example: for the text "a#bc# -#", set backreferences with a, c and -. You are not allowed to consume the hash character.

	参考: /(?=.#)(.)/g
	代码: re.findall(r"(?=.#)(?P<tag>.)", "...", re.S)

## Task 11: Validate Floating Point Numbers ##

	Check if a floating point number (e.g. 3.14159) is in a valid format.

	参考: /^[-+]?(?:\d*[\.,]?\d+|\d+[.,])(?:[eE][-+]?\d+)?$/g
	代码: re.findall(r"^[-+]?(?:\d*[\.,]?\d+|\d+[.,])(?:[eE][-+]?\d+)?$", "...", re.S)

## Task 12: Match any number between 0-100 ##

	Could you help me validate my input and only match positive integers between the range of 0 and 100? There can be several numbers in a string which I would want to retrieve. Try out these example strings: Sam has 200 apples. He gives Todd 20 and Mary 125. and The weather is -5 C today, but will be +5 C tomorrow.

	参考: /(?:\+|^|\s)(?:\d|[1-9]\d|100)(?:\s|$)/g
	代码: re.findall(r"(?:\+|^|\s)(?:\d|[1-9]\d|100)(?:\s|$)", "...", re.S)

## Task 13: Match alternating 0s and 1s in any order ##

	I'm trying to match bit sequences which are alternating between 1 and 0 and never have more than one 1 or 0 in a row. They can be single digits. Try matching this: 0101010, 1010101010 or 1

	参考: /\b(?:10?|1?(?:01)+0?|01?)\b/g
	代码: re.findall(r"\b(?:10?|1?(?:01)+0?|01?)\b", "...", re.S)

## Task 14: Spam Filter ##

	Match a string that contains any of the following substrings: http://, www., porn, or credit card. But don't match the text if it contains one of: not allowed, filter, or mirc. Don't use word boundaries (anywhere in the text is fine). If you need help, try reading this.

	参考: /^(?!.*(?:not allowed|filter|mirc).*).*(?:http:\/\/|www\.|porn|credit card).*$/i
	代码: re.search(r"^(?!.*(?:not allowed|filter|mirc).*).*(?:http://|www\.|porn|credit card).*$", "...", re.IGNORECASE)

## Task 15: Not Surrounded By Digits ##

	Replace every . (dot) with a - (hyphen) except when the dot is surrounded by digits. E.g.: .a.b.1.2. should become -a-b-1.2-

	参考: s/(?!\.\d)\.|\.(?<!\d\.)/-/g
	代码: re.sub(r"(?!\.\d)\.|\.(?<!\d\.)", "-", "...", flags=re.S)

## Task 16: Repeated Words ##

	I'd like to know if a text contains words with 4 characters or more which are repeated 3 or more times in the text (anywhere in the text). If so, set one (and only one) backreference for each word.

	参考: /(?=(\b\w{4,}\b)(?:.*?\b\1\b.*?){2})(?!(\b\w{4,}\b)(?:.*?\b\1\b.*?){3})/ig
	代码: re.findall(r"(?=(\b\w{4,}\b)(?:.*?\b\1\b.*?){2})(?!(\b\w{4,}\b)(?:.*?\b\1\b.*?){3})", "...", re.S)

## Task 17: Start before End ##

	Only match lines with the text start, unless the text end is before that (end may or may not be in the string). Match: ssstarttt line And don't match line_end start

	参考: /^(?:(?!end).)*start.*/g
	代码: re.findall(r"^(?:(?!end).)*start.*", "...", re.S)

## Task 18: Every other digit ##

	Replace every other character if it's a \d with * (only those in even positions: 2, 4, 6, etc). Example: a1b2cde3~g45hi6 should become a*b*cde*~g4*hi6

	参考: s/\G((?:.\D)*.)\d/$1*/g
	代码: Python正则没有\G

## Task 19: The Thousands ##

	Use substitution to put commas in all numbers to separate the thousands. ie: 12345678 → 12,345,678. The number could be in a sentence, and there may be more than one number in the sentence.

	参考: s/(?<![a-zA-Z])(?<![a-zA-Z]\d|\d[a-zA-Z])(?<!\d[a-zA-Z]\d|[a-zA-Z]\d\d|\d\d[a-zA-Z])(\d)(?=(?:\d{3})+\b)/$1,/g
	参考: s/(?=\b\d|\G)\d+?(?=(?:\d{3})+\b)/$0,/g
	代码: re.sub(r"(?<![a-zA-Z])(?<![a-zA-Z]\d|\d[a-zA-Z])(?<!\d[a-zA-Z]\d|[a-zA-Z]\d\d|\d\d[a-zA-Z])(\d)(?=(?:\d{3})+\b)", r"\1,", "...", flags=re.S)

## Task 20: Quoted Text With Escapes ##

	Validate a line in quotes. Return one (and only one) backreference with the text. ie: quoted text from "quoted text". Note: a \ escapes any char, so \" is a valid escape.

	参考: /^"(?:[^"\\]*(?:\\.)*[^"\\]*)*"$/
	参考: /^"((?:[^"\\]*(?:\\.)*)*)"$/
	代码: re.findall(r'"((?:[^"\\]*(?:\\.)*)*)"$', '...', re.S)

## Task 21: Replace Text, Not Code ##

	In an HTML page, replace the text micro with &micro;. Oh, and don't screw up the code: don't replace inside <the tags> or &entities;

	参考: s/(?:<.*?>|&\w++;)(*SKIP)(*F)|micro/&micro;/g
	代码: Python正则没有SKIP
