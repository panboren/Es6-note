1
let 命令:

let声明的变量只在它所在的代码块有效。

let命令改变了语法行为，它所声明的变量一定要在声明后使用

如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

变量一定要在声明之后使用，否则就报错。

let不允许在相同作用域内，重复声明同一个变量

不能在函数内部重新声明参数。

2
ES6 的块级作用域

ES6 允许块级作用域的任意嵌套。
外层作用域无法读取内层作用域的变量。

内层作用域可以定义外层作用域的同名变量。

3
const 命令
const声明一个只读的常量。一旦声明，常量的值就不能改变

const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。

对于const来说，只声明不赋值，就会报错。

const命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。

const声明的常量，也与let一样不可重复声明。

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。


ES6 声明变量的六种方法
ES5 只有两种声明变量的方法：var命令和function命令。ES6 除了添加let和const命令，后面章节还会提到，另外两种声明变量的方法：import命令和class命令。所以，ES6 一共有 6 种声明变量的方法。


第三课
变量的解构赋值

可以从数组中提取值，按照对应位置，对变量赋值

只要等号两边的模式相同，左边的变量就会被赋予对应的值。

如果等号的右边不是数组，那么将会报错。

对于 Set 结构，也可以使用数组的解构赋值。

解构赋值允许指定默认值。

如果解构不成功，变量的值就等于undefined。

因为等号右边的值，要么转为对象以后不具备 Iterator 接口（前五个表达式），要么本身就不具备 Iterator 接口（最后一个表达式）。

只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。

如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

默认值可以引用解构赋值的其他变量，但该变量必须已经声明。

二对象的解构赋值

对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值

对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

默认值生效的条件是，对象的属性值严格等于undefined。

如果解构失败，变量的值等于undefined。

如果解构模式是嵌套的对象，而且子对象所在的父属性不存在，那么将会报错。

只有不将大括号写在行首，避免 JavaScript 将其解释为代码块，才能解决这个问题。（用括号包起来）

解构赋值允许等号左边的模式之中，不放置任何变量名。因此，可以写出非常古怪的赋值表达式。

由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

方括号这种写法，属于“属性名表达式”

字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。

类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。

解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。

函数的参数也可以使用解构赋值。

undefined就会触发函数参数的默认值。

建议只要有可能，就不要在模式中放置圆括号。

变量声明语句，模式不能使用圆括号。

赋值语句的非模式部分，可以使用圆括号


第四课字符串扩展

 如果直接在\u后面跟上超过0xFFFF的数值。只要将码点放入大括号，就能正确解读该字符。

大括号表示法与四字节的 UTF-16 编码是等价的。

codePointAt()
ES6 提供了codePointAt方法，能够正确处理 4 个字节储存的字符，返回一个字符的码点。

codePointAt方法返回的是码点的十进制值，如果想要十六进制的值，可以使用toString方法转换一下。

使用for...of循环，因为它会正确识别 32 位的 UTF-16 字符。

codePointAt方法是测试一个字符由两个字节还是由四个字节组成的最简单方法。c.codePointAt(0) > 0xFFFF;

String.fromCodePoint()
可以识别大于0xFFFF的字符，弥补了String.fromCharCode方法的不足。在作用上，正好与codePointAt方法相反。

如果String.fromCodePoint方法有多个参数，则它们会被合并成一个字符串返回。

注意，fromCodePoint方法定义在String对象上，而codePointAt方法定义在字符串的实例对象上。

for...of循环遍历。可以识别大于0xFFFF的码点，传统的for循环无法识别这样的码点。

at方法，可以识别 Unicode 编号大于0xFFFF的字符，返回正确的字符。'??'.at(0) // "??"

includes()：返回布尔值，表示是否找到了参数字符串。
startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
这三个方法都支持第二个参数，表示开始搜索的位置。
endsWith的行为与其他两个方法有所不同。它针对前n个字符，而其他两个方法针对从第n个位置直到字符串结束。

repeat方法返回一个新字符串，表示将原字符串重复n次。
参数如果是小数，会被取整。
如果repeat的参数是负数或者Infinity，会报错。
如果参数是 0 到-1 之间的小数，则等同于 0，这是因为会先进行取整运算。0 到-1 之间的小数，取整以后等于-0，repeat视同为 0。
参数NaN等同于 0。
如果repeat的参数是字符串，则会先转换成数字

padStart()用于头部补全，padEnd()用于尾部补全。
第一个参数用来指定字符串的最小长度，第二个参数是用来补全的字符串。
如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串
如果用来补全的字符串与原字符串，两者的长度之和超过了指定的最小长度，则会截去超出位数的补全字符串。
如果省略第二个参数，默认使用空格补全长度。

matchAll方法返回一个正则表达式在当前字符串的所有匹配

模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。
如果在模板字符串中需要使用反引号，则前面要用反斜杠转义。

如果使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中
如果你不想要这个换行，可以使用trim方法消除它

模板字符串中嵌入变量，需要将
变量名写在${}之中。

大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性。

模板字符串之中还能调用函数。

如果大括号中的值不是字符串，将按照一般的规则转为字符串
默认调用对象的toString方法

如果模板字符串中的变量没有声明，将报错。
如果大括号内部是一个字符串，将会原样输出。

模板字符串甚至还能嵌套。

标签模板其实不是模板，而是函数调用的一种特殊形式。“标签”指的就是函数，紧跟在后面的模板字符串就是它的参数。

tag函数的第一个参数是一个数组，该数组的成员是模板字符串中那些没有变量替换的部分，也就是说，变量替换只发生在数组的第一个成员与第二个成员之间、第二个成员与第三个成员之间，以此类推。

tag函数的其他参数，都是模板字符串各个变量被替换后的值。由于本例中，模板字符串含有两个变量，因此tag会接受到value1和value2两个参数。

String.raw方法，往往用来充当模板字符串的处理函数，返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，对应于替换变量后的模板字符串。


第五课正则的扩展

RegExp构造函数第一个参数是一个正则对象，那么可以使用第二个参数指定修饰符。而且，返回的正则表达式会忽略原有的正则表达式的修饰符，只使用新指定的修饰符。flags

字符串对象共有 4 个方法，可以使用正则表达式：match()、replace()、search()和split()。

对于码点大于0xFFFF的 Unicode 字符，点字符不能识别，必须加上u修饰符。

正则表达式中必须加上u修饰符，才能识别当中的大括号，否则会被解读为量词。

使用u修饰符后，所有量词都会正确识别码点大于0xFFFF的 Unicode 字符。

y修饰符，叫做“粘连”（sticky）修饰符。

y修饰符确保匹配必须从剩余的第一个位置开始，这也就是“粘连”的涵义。

sticky属性，表示是否设置了y修饰符

flags属性，会返回正则表达式的修饰符。


所谓行终止符，就是该字符表示一行的终结。以下四个字符属于”行终止符“。

U+000A 换行符（\n）
U+000D 回车符（\r）
U+2028 行分隔符（line separator）
U+2029 段分隔符（paragraph separator）

dotAll模式，即点（dot）代表一切字符。所以，正则表达式还引入了一个dotAll属性，返回一个布尔值，表示该正则表达式是否处在dotAll模式

二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。

第六课数值的扩展
Number.isFinite()用来检查一个数值是否为有限的（finite），即不是Infinity。

注意，如果参数类型不是数值，Number.isFinite一律返回false

Number.isNaN()用来检查一个值是否为NaN。

注意，如果参数类型不是数值，Number.isNaN一律返回false。

全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。

Number.isInteger()用来判断一个数值是否为整数。

Number.isInteger返回false。

在Number对象上面，新增一个极小的常量Number.EPSILON

Number.MAX_SAFE_INTEGER和Number.MIN_SAFE_INTEGER这两个常量，用来表示这个范围的上下限

Number.isSafeInteger()则是用来判断一个整数是否落在这个范围之内。


Math.trunc方法用于去除一个数的小数部分，返回整数部分。

Math.trunc内部使用Number方法将其先转为数值

对于空值和无法截取整数的值，返回NaN

Math.sign方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。
它会返回五种值。

参数为正数，返回+1；
参数为负数，返回-1；
参数为 0，返回0；
参数为-0，返回-0;
其他值，返回NaN。

如果参数是非数值，会自动转为数值。对于那些无法转为数值的值，会返回NaN。

Math.cbrt方法用于计算一个数的立方根。

对于非数值，Math.cbrt方法内部也是先使用Number方法将其转为数值。

Math.clz32方法返回一个数的 32 位无符号整数形式有多少个前导 0。

对于小数，Math.clz32方法只考虑整数部分。

对于空值或其他类型的值，Math.clz32方法会将它们先转为数值，然后再计算

Math.imul方法返回两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数

Math.fround方法返回一个数的32位单精度浮点数形式

Math.hypot方法返回所有参数的平方和的平方根。

*************************************************************
第七课函数的扩展

允许为函数的参数设置默认值，即直接写在参数定义的后面。

参数变量是默认声明的，所以不能用let或const再次声明

使用参数默认值时，函数不能有同名参数。

参数默认值是惰性求值的。

参数默认值可以与解构赋值的默认值，结合起来使用。

如果非尾部的参数设置默认值，实际上这个参数是没法省略的。

有默认值的参数都不是尾参数。这时，无法只省略该参数，而不省略它后面的参数，除非显式输入undefined。

如果传入undefined，将触发该参数等于默认值，null则没有这个效果。

length属性的返回值，等于函数的参数个数减去指定了默认值的参数个数。

如果设置了默认值的参数不是尾参数，那么length属性也不再计入后面的参数了。

一旦设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域（context）。等到初始化结束，这个作用域就会消失。这种语法行为，在不设置参数默认值时，是不会出现的。

rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

rest 参数就是一个真正的数组

rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

函数的length属性，不包括 rest 参数。

规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。

第一种是设定全局性的严格模式，这是合法的。

第二种是把函数包在一个无参数的立即执行函数里面。

函数的name属性，返回该函数的函数名。

ES5 的name属性，会返回空字符串，而 ES6 的name属性会返回实际的函数名。

如果将一个具名函数赋值给一个变量，则 ES5 和 ES6 的name属性都返回这个具名函数原本的名字。


Function构造函数返回的函数实例，name属性的值为anonymous。

bind返回的函数，name属性值会加上bound前缀。


如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分。

如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。

由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错。

箭头函数可以与变量解构结合使用。

箭头函数的一个用处是简化回调函数。

使用注意点
箭头函数有几个使用注意点。

（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。


除了this，以下三个变量在箭头函数之中也是不存在的，指向外层函数的对应变量：arguments、super、new.target。

由于箭头函数没有自己的this，所以当然也就不能用call()、apply()、bind()这些方法去改变this的指向。


函数绑定运算符是并排的两个冒号（::），双冒号左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。

如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面。

如果双冒号运算符的运算结果，还是一个对象，就可以采用链式写法。

尾调用就是指某个函数的最后一步是调用另一个函数。

尾调用优化”的意义节省内存

注意，只有不再用到外层函数的内部变量，内层函数的调用帧才会取代外层函数的调用帧，否则就无法进行“尾调用优化”。

函数调用自身，称为递归。如果尾调用自身，就称为尾递归。

尾递归的实现，往往需要改写递归函数，确保最后一步只调用自身。做到这一点的方法，就是把所有用到的内部变量改写成函数的参数。


***************************************************
八课数组的扩展

扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

如果扩展运算符后面是一个空数组，则不产生任何效果。

扩展运算符后面还可以放置表达式。

由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了。


如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错。

凡是涉及到操作四个字节的 Unicode 字符的函数，都有这个问题。因此，最好都用扩展运算符改写。

Array.from方法用于将两类对象转为真正的数组


值得提醒的是，扩展运算符（...）也可以将某些数据结构转为数组。


扩展运算符背后调用的是遍历器接口（Symbol.iterator），如果一个对象没有部署这个接口，就无法转换。Array.from方法还支持类似数组的对象。所谓类似数组的对象，本质特征只有一点，即必须有length属性。因此，任何有length属性的对象，都可以通过Array.from方法转为数组，而此时扩展运算符就无法转换。

Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。


如果map函数里面用到了this关键字，还可以传入Array.from的第三个参数，用来绑定this。


Array.of方法用于将一组值，转换为数组。

Array.of总是返回参数值组成的数组。如果没有参数，就返回一个空数组。

数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
它接受三个参数。

target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。
end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
这三个参数都应该是数值，如果不是，会自动转为数值。

数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。
find方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

这两个方法都可以接受第二个参数，用来绑定回调函数的this对象。

另外，这两个方法都可以发现NaN，弥补了数组的indexOf方法的不足。

fill方法使用给定值，填充一个数组。
fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。

注意，如果填充的类型为对象，那么被赋值的是同一个内存地址的对象，而不是深拷贝对象。

ES6 提供三个新的方法——entries()，keys()和values()——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。

数组实例的 includes()
表示某个数组是否包含给定的值，与字符串的includes方法类似

该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。

Map 和 Set 数据结构有一个has方法，需要注意与includes区分。
Map 结构的has方法，是用来查找键名的
Set 结构的has方法，是用来查找值的

Array.from方法会将数组的空位，转为undefined
扩展运算符（...）也会将空位转为undefined。
copyWithin()会连空位一起拷贝。
fill()会将空位视为正常的数组位置。
for...of循环也会遍历空位。

entries()、keys()、values()、find()和findIndex()会将空位处理成undefined。


***************************
第九课对象的扩展

允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。

属性的赋值器（setter）和取值器（getter），事实上也是采用这种写法。

注意，简洁写法的属性名总是字符串，这会导致一些看上去比较奇怪的结果

如果某个方法的值是一个 Generator 函数，前面需要加上星号。

ES6 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。

注意，属性名表达式与简洁表示法，不能同时使用，会报错。

注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心。

函数的name属性，返回函数名。对象方法也是函数，因此也有name属性。

如果对象的方法使用了取值函数（getter）和存值函数（setter），则name属性不是在该方法上面，而是该方法的属性的描述对象的get和set属性上面，返回值是方法名前加上get和set。

有两种特殊情况：bind方法创造的函数，name属性返回bound加上原函数的名字；Function构造函数创造的函数，name属性返回anonymous。

对象的方法是一个 Symbol 值，那么name属性返回的是这个 Symbol 值的描述。

Object.is就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

不同之处只有两个：一是+0不等于-0，二是NaN等于自身。

Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。
Object.assign方法的第一个参数是目标对象，后面的参数都是源对象

注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。
如果该参数不是对象，则会先转成对象，然后返回
如果只有一个参数，Object.assign会直接返回该参数。
由于undefined和null无法转成对象，所以如果它们作为参数，就会报错。

如果非对象参数出现在源对象的位置（即非首参数），那么处理规则有所不同。首先，这些参数都会转成对象，如果无法转成对象，就会跳过。这意味着，如果undefined和null不在首参数，就不会报错。

其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果

Object.assign拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（enumerable: false）。

属性名为 Symbol 值的属性，也会被Object.assign拷贝。

Object.assign方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用


一旦遇到同名属性，Object.assign的处理方法是替换，而不是添加。

Object.assign可以用来处理数组，但是会把数组视为对象。

Object.assign只能进行值的复制，如果要复制的值是一个取值函数，那么将求值后再复制。

Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象。


有四个操作会忽略enumerable为false的属性。

for...in循环：只遍历对象自身的和继承的可枚举的属性。
Object.keys()：返回对象自身的所有可枚举的属性的键名。
JSON.stringify()：只串行化对象自身的可枚举的属性。
Object.assign()： 忽略enumerable为false的属性，只拷贝对象自身的可枚举的属性。


Object.getOwnPropertyDescriptor方法会返回某个对象属性的描述对象（descriptor）。ES2017 引入了Object.getOwnPropertyDescriptors方法，返回指定对象所有自身属性（非继承属性）的描述对象。


ES6 规定，所有 Class 的原型的方法都是不可枚举的。

ES6 一共有 5 种方法可以遍历对象的属性。

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

首先遍历所有数值键，按照数值升序排列。
其次遍历所有字符串键，按照加入时间升序排列。
最后遍历所有 Symbol 键，按照加入时间升序排列。


Object.getOwnPropertyDescriptors方法返回一个对象，所有原对象的属性名都是该对象的属性名，对应的属性值就是该属性的描述对象。

Object.assign方法总是拷贝一个属性的值，而不会拷贝它背后的赋值方法或取值方法。


__proto__属性（前后各两个下划线），用来读取或设置当前对象的prototype对象。

Object.setPrototypeOf方法的作用与__proto__相同，用来设置一个对象的prototype对象，返回参数对象本身。

如果第一个参数不是对象，会自动转为对象。但是由于返回的还是第一个参数，所以这个操作不会产生任何效果。

由于undefined和null无法转为对象，所以如果第一个参数是undefined或null，就会报错。

Object.getPrototypeOf()用于读取一个对象的原型对象。

ES6 又新增了另一个类似的关键字super，指向当前对象的原型对象。

注意，super关键字表示原型对象时，只能用在对象的方法之中，用在其他地方都会报错。

ES5 引入了Object.keys方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

ES2017 引入了跟Object.keys配套的Object.values和Object.entries，作为遍历一个对象的补充手段，供for...of循环使用。

Object.values方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。

如果参数不是对象，Object.values会先将其转为对象。由于数值和布尔值的包装对象，都不会为实例添加非继承的属性。所以，Object.values会返回空数组

Object.entries方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。

扩展运算符的解构赋值，不能复制继承自原型对象的属性。
注意，解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数）、那么解构赋值拷贝的是这个值的引用，而不是这个值的副本。


***************************
**************
第十课Symbol

ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值

Symbol 值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

注意，Symbol函数前不能使用new命令，否则会报错。这是因为生成的 Symbol 是一个原始类型的值，不是对象。也就是说，由于 Symbol 值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。


注意，Symbol函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的Symbol函数的返回值是不相等的。

Symbol 值不能与其他类型的值进行运算，会报错。

Symbol 值也可以转为布尔值，但是不能转为数值。

由于每一个 Symbol 值都是不相等的，这意味着 Symbol 值可以作为标识符，用于对象的属性名，就能保证不会出现同名的属性。这对于一个对象由多个模块构成的情况非常有用，能防止某一个键被不小心改写或覆盖。

注意，Symbol 值作为对象属性名时，不能用点运算符。
因为点运算符后面总是字符串，所以不会读取mySymbol作为标识名所指代的那个值

同理，在对象的内部，使用 Symbol 值定义属性时，Symbol 值必须放在方括号之中。
Symbol 值作为属性名时，该属性还是公开属性，不是私有属性。

魔术字符串指的是，在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值。风格良好的代码，应该尽量消除魔术字符串，改由含义清晰的变量代替。

Symbol 作为属性名，该属性不会出现在for...in、for...of循环中，也不会被Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回。但是，它也不是私有属性，有一个Object.getOwnPropertySymbols方法，可以获取指定对象的所有 Symbol 属性名。

Reflect.ownKeys方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。

我们希望重新使用同一个 Symbol 值，Symbol.for方法可以做到这一点。

都是同样参数的Symbol.for方法生成的，所以实际上是同一个值。

Symbol.keyFor方法返回一个已登记的 Symbol 类型值的key。

Singleton 模式指的是调用一个类，任何时候返回的都是同一个实例。

**
内置的 Symbol 值

对象的Symbol.hasInstance属性，指向一个内部方法。当其他对象使用instanceof运算符，判断是否为该对象的实例时，会调用这个方法

对象的Symbol.isConcatSpreadable属性等于一个布尔值，表示该对象用于Array.prototype.concat()时，是否可以展开。

对象的Symbol.species属性，指向一个构造函数。创建衍生对象时，会使用该属性。

对象的Symbol.match属性，指向一个函数。当执行str.match(myObject)时，如果该属性存在，会调用它，返回该方法的返回值。

对象的Symbol.replace属性，指向一个方法，当该对象被String.prototype.replace方法调用时，会返回该方法的返回值。

对象的Symbol.search属性，指向一个方法，当该对象被String.prototype.search方法调用时，会返回该方法的返回值。

对象的Symbol.split属性，指向一个方法，当该对象被String.prototype.split方法调用时，会返回该方法的返回值。

对象的Symbol.iterator属性，指向该对象的默认遍历器方法。

对象的Symbol.toPrimitive属性，指向一个方法。该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。

Symbol.toPrimitive被调用时，会接受一个字符串参数，表示当前运算的模式，一共有三种模式。

Number：该场合需要转成数值
String：该场合需要转成字符串
Default：该场合可以转成数值，也可以转成字符串

对象的Symbol.toStringTag属性，指向一个方法。在该对象上面调用Object.prototype.toString方法时，如果这个属性存在，它的返回值会出现在toString方法返回的字符串之中，表示对象的类型。也就是说，这个属性可以用来定制[object Object]或[object Array]中object后面的那个字符串。

对象的Symbol.unscopables属性，指向一个对象。该对象指定了使用with关键字时，哪些属性会被with环境排除。

************************************************
第十一课Set和Map数据结构

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值

Set 函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。
向 Set 加入值的时候，不会发生类型转换
Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于精确相等运算符（===），主要的区别是NaN等于自身，而精确相等运算符认为NaN不等于自身。

在 Set 内部，两个NaN是相等。
两个对象总是不相等的。


Set 结构的实例有以下属性。

Set.prototype.constructor：构造函数，默认就是Set函数。
Set.prototype.size：返回Set实例的成员总数。

Array.from方法可以将 Set 结构转为数组。

四个操作方法。
add(value)：添加某个值，返回 Set 结构本身。
delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
has(value)：返回一个布尔值，表示该值是否为Set的成员。
clear()：清除所有成员，没有返回值。

Set 结构的实例有四个遍历方法，可以用于遍历成员。

keys()：返回键名的遍历器
values()：返回键值的遍历器
entries()：返回键值对的遍历器
forEach()：使用回调函数遍历每个成员

Set 结构的实例默认可遍历，它的默认遍历器生成函数就是它的values方法。
这意味着，可以省略values方法，直接用for...of循环遍历 Set。

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。
forEach方法还可以有第二个参数，表示绑定处理函数内部的this对象。

扩展运算符（...）内部使用for...of循环，所以也可以用于 Set 结构。

数组的map和filter方法也可以间接用于 Set 了。

***
WeakSet
WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。

首先，WeakSet 的成员只能是对象，而不能是其他类型的值。

WeakSet 中的对象都是弱引用WeakSet 适合临时存放一组对象，以及存放跟对象绑定的信息。只要这些对象在外部消失，它在 WeakSet 里面的引用就会自动消失。

WeakSet 不可遍历

WeakSet 是一个构造函数，可以使用new命令，创建 WeakSet 数据结构。

WeakSet 可以接受一个数组或类似数组的对象作为参数。（实际上，任何具有 Iterable 接口的对象，都可以作为 WeakSet 的参数。）该数组的所有成员，都会自动成为 WeakSet 实例对象的成员。

注意，是a数组的成员成为 WeakSet 的成员，而不是a数组本身。这意味着，数组的成员只能是对象。
WeakSet.prototype.add(value)：向 WeakSet 实例添加一个新成员。
WeakSet.prototype.delete(value)：清除 WeakSet 实例的指定成员。
WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。
WeakSet 没有size属性，没有办法遍历它的成员。

WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。

*******
*********
Map

Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

Map 也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。

不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作Map构造函数的参数。这就是说，Set和Map都可以用来生成新的 Map。

如果对同一个键多次赋值，后面的值将覆盖前面的值。

如果读取一个未知的键，则返回undefined。

Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。

undefined和null也是两个不同的键。虽然NaN不严格相等于自身，但 Map 将其视为同一个键。

Map 结构的实例有以下属性和操作方法
size属性返回 Map 结构的成员总数。

set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该键。

set方法返回的是当前的Map对象，因此可以采用链式写法。

get方法读取key对应的键值，如果找不到key，返回undefined。

has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中

delete方法删除某个键，返回true。如果删除失败，返回false。

clear方法清除所有成员，没有返回值。

Map 结构原生提供三个遍历器生成函数和一个遍历方法。

keys()：返回键名的遍历器。
values()：返回键值的遍历器。
entries()：返回所有成员的遍历器。
forEach()：遍历 Map 的所有成员。

Map 结构的默认遍历器接口（Symbol.iterator属性），就是entries方法。

Map 结构转为数组结构，比较快速的方法是使用扩展运算符（...）。

*****
WeakMap
WeakMap结构与Map结构类似，也是用于生成键值对的集合。

WeakMap与Map的区别有两点。

首先，WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。

WeakMap的键名所指向的对象，不计入垃圾回收机制。

一旦不再需要，WeakMap 里面的键名对象和所对应的键值对会自动消失，不用手动删除引用。

基本上，如果你要往对象上添加数据，又不想干扰垃圾回收机制，就可以使用 WeakMap

注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用。

WeakMap 与 Map 在 API 上的区别主要是两个，一是没有遍历操作（即没有key()、values()和entries()方法），也没有size属性

WeakMap只有四个方法可用：get()、set()、has()、delete()。

****************************************************
第十二课Proxy

Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。

Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

Proxy 对象的所有用法，都是上面这种形式，不同的只是handler参数的写法。其中，new Proxy()表示生成一个Proxy实例，target参数表示所要拦截的目标对象，handler参数也是一个对象，用来定制拦截行为。


Proxy接受两个参数。
第一个参数是所要代理的目标对象.
第二个参数是一个配置对象，对于每一个被代理的操作，需要提供一个对应的处理函数，该函数将拦截对应的操作。

注意，要使得Proxy起作用，必须针对Proxy实例（上例是proxy对象）进行操作，而不是针对目标对象（上例是空对象）进行操作。

一个技巧是将 Proxy 对象，设置到object.proxy属性，从而可以在object对象上调用。

Proxy 支持的拦截操作一览，一共 13 种。

get(target, propKey, receiver)：拦截对象属性的读取

set(target, propKey, value, receiver)：拦截对象属性的设置

has(target, propKey)：拦截propKey in proxy的操作

deleteProperty(target, propKey)：拦截delete proxy[propKey]的操作

ownKeys(target)：

getOwnPropertyDescriptor(target, propKey)：

defineProperty(target, propKey, propDesc)：

preventExtensions(target)

getPrototypeOf(target)

isExtensible(target)

setPrototypeOf(target, proto)

apply(target, object, args)

construct(target, args)

get方法用于拦截某个属性的读取操作，可以接受三个参数，依次为目标对象、属性名和 proxy 实例本身（即this关键字指向的那个对象），其中最后一个参数可选。

set方法用来拦截某个属性的赋值操作，可以接受四个参数，依次为目标对象、属性名、属性值和 Proxy 实例本身，其中最后一个参数可选。

apply方法拦截函数的调用、call和apply操作。

apply方法可以接受三个参数，分别是目标对象、目标对象的上下文对象（this）和目标对象的参数数组。

has方法用来拦截HasProperty操作，即判断对象是否具有某个属性时，这个方法会生效。典型的操作就是in运算符。
	 。
	 。
	 。

this 问题：
主要原因就是在 Proxy 代理的情况下，目标对象内部的this关键字会指向 Proxy 代理。


第十三课Reflect

（1） 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），放到Reflect对象上。现阶段，某些方法同时在Object和Reflect对象上部署，未来的新方法将只部署在Reflect对象上。也就是说，从Reflect对象上可以拿到语言内部的方法。

（2） 修改某些Object方法的返回结果，让其变得更合理。比如，Object.defineProperty(obj, name, desc)在无法定义属性时，会抛出一个错误，而Reflect.defineProperty(obj, name, desc)则会返回false。

（3） 让Object操作都变成函数行为。某些Object操作是命令式，比如name in obj和delete obj[name]，而Reflect.has(obj, name)和Reflect.deleteProperty(obj, name)让它们变成了函数行为。

（4）Reflect对象的方法与Proxy对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为。

Reflect对象一共有 13 个静态方法。

Reflect.apply(target, thisArg, args)
Reflect.construct(target, args)
Reflect.get(target, name, receiver)
Reflect.set(target, name, value, receiver)
Reflect.defineProperty(target, name, desc)
Reflect.deleteProperty(target, name)
Reflect.has(target, name)
Reflect.ownKeys(target)
Reflect.isExtensible(target)
Reflect.preventExtensions(target)
Reflect.getOwnPropertyDescriptor(target, name)
Reflect.getPrototypeOf(target)
Reflect.setPrototypeOf(target, prototype)


-********************************
第十四课 Promise

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大


从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

Promise对象有以下两个特点。

（1）对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。


Promise对象是一个构造函数，用来生成Promise实例。


Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。

then方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受Promise对象传出的值作为参数。

then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行

Promise 实例具有then方法，也就是说，then方法是定义在原型对象Promise.prototype上的。它的作用是为 Promise 实例添加状态改变时的回调函数。前面说过，then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数。


Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数。

一般来说，不要在then方法里面定义 Reject 状态的回调函数（即then的第二个参数），总是使用catch方法。

Promise 内部的错误不会影响到 Promise 外部的代码，通俗的说法就是“Promise 会吃掉错误”。

Promise.prototype.finally()
finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作

Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

Promise.all方法接受一个数组作为参数，

（Promise.all方法的参数可以不是数组，但必须具有 Iterator 接口，且返回的每个成员都是 Promise 实例。）

（1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。

（2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。


Promise.race方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。

Promise.race方法的参数与Promise.all方法一样，如果不是 Promise 实例，就会先调用下面讲到的Promise.resolve方法，将参数转为 Promise 实例，再进一步处理。

有时需要将现有对象转为 Promise 对象，Promise.resolve方法就起到这个作用。
（1）参数是一个 Promise 实例
（2）参数是一个thenable对象
（3）参数不是具有then方法的对象，或根本就不是对象
（4）不带有任何参数

Promise.reject(reason)方法也会返回一个新的 Promise 实例，该实例的状态为rejected。

注意，Promise.reject()方法的参数，会原封不动地作为reject的理由，变成后续方法的参数。这一点与Promise.resolve方法不一致。


Promise.try()

第十五课Iterator和for...of循环

Iterator（遍历器）的概念

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

Iterator 的遍历过程是这样的。

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的next方法，直到它指向数据结构的结束位置。


原生具备 Iterator 接口的数据结构如下。

Array
Map
Set
String
TypedArray
函数的 arguments 对象
NodeList 对象


ES6 的有些数据结构原生具备 Iterator 接口（比如数组），即不用任何处理，就可以被for...of循环遍历。原因在于，这些数据结构原生部署了Symbol.iterator属性


第十六课Genetator

Generator 函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同


Generator 函数有多种理解角度。语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。

Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同的内部状态（yield在英语里的意思就是“产出”）。

Generator 函数的调用方法与普通函数一样,函数名后面加上一对圆括号。调用 Generator 函数后，该函数并不执行,返回的也不是函数运行结果，而是一个指向内部状态的指针对象，遍历器对象（Iterator Object）。下一步，必须调用遍历器对象的next方法，使得指针移向下一个状态。Generator 函数是分段执行的，yield表达式是暂停执行的标记，而next方法可以恢复执行

总结一下，调用 Generator 函数，返回一个遍历器对象，代表 Generator 函数的内部指针。以后，每次调用遍历器对象的next方法，就会返回一个有着value和done两个属性的对象。value属性表示当前的内部状态的值，是yield表达式后面那个表达式的值；done属性是一个布尔值，表示是否遍历结束。

由于 Generator 函数仍然是普通函数，即星号紧跟在function关键字后面。


yield 表达式

只有调用next方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。yield表达式就是暂停标志。

遍历器对象的next方法的运行逻辑如下。

（1）遇到yield表达式，就暂停执行后面的操作，并将紧跟在yield后面的那个表达式的值，作为返回的对象的value属性值。
（2）下一次调用next方法时，再继续往下执行，直到遇到下一个yield表达式。
（3）如果没有再遇到新的yield表达式，就一直运行到函数结束，直到return语句为止，并将return语句后面的表达式的值，作为返回的对象的value属性值。

（4）如果该函数没有return语句，则返回的对象的value属性值为undefined。


需要注意的是，yield表达式后面的表达式，只有当调用next方法、内部指针指向该语句时才会执行，因此等于为 JavaScript 提供了手动的“惰性求值”（Lazy Evaluation）的语法功能。

会在next方法将指针移到这一句时，才会求值。

Generator 函数可以不用yield表达式，这时就变成了一个单纯的暂缓执行函数

另外需要注意，yield表达式只能用在 Generator 函数里面，用在其他地方都会报错。

另外，yield表达式如果用在另一个表达式之中，必须放在圆括号里面。

yield表达式用作函数参数或放在赋值表达式的右边，可以不加括号。

next 方法的参数
next方法可以带一个参数，该参数就会被当作上一个yield表达式的返回值。

注意，由于next方法的参数表示上一个yield表达式的返回值，所以在第一次使用next方法时，传递参数是无效的。V8 引擎直接忽略第一次使用next方法时的参数，只有从第二次使用next方法开始，参数才是有效的。从语义上讲，第一个next方法用来启动遍历器对象，所以不用带有参数。

一旦next方法的返回对象的done属性为true，for...of循环就会中止，且不包含该返回对象，


for...of循环可以自动遍历 Generator 函数时生成的Iterator对象，且此时不再需要调用next方法。


一旦next方法的返回对象的done属性为true，for...of循环就会中止，且不包含该返回对象，所以上面代码的return语句返回的6，不包括在for...of循环之中。


Generator.prototype.throw()
Generator 函数返回的遍历器对象，都有一个throw方法，可以在函数体外抛出错误，然后在 Generator 函数体内捕获。

Generator.prototype.return() § ?
Generator 函数返回的遍历器对象，还有一个return方法，可以返回给定的值，并且终结遍历 Generator 函数。

next()、throw()、return()这三个方法本质上是同一件事，可以放在一起理解。它们的作用都是让 Generator 函数恢复执行，并且使用不同的语句替换yield表达式。

next()是将yield表达式替换成一个值。

throw()是将yield表达式替换成一个throw语句。
return()是将yield表达式替换成一个return语句。

yield* 表达式


这个就需要用到yield*表达式，用来在一个 Generator 函数里面执行另一个 Generator 函数。

第十七课Generator 函数的异步应用

协程有点像函数，又有点像线程。它的运行流程大致如下。

第一步，协程A开始执行。
第二步，协程A执行到一半，进入暂停，执行权转移到协程B。
第三步，（一段时间后）协程B交还执行权。
第四步，协程A恢复执行。



编译器的“传名调用”实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做 Thunk 函数。


第十八课
它就是 Generator 函数的语法糖

async函数就是将 Generator 函数的星号（*）替换成async，将yield替换成await，仅此而已。

async函数对 Generator 函数的改进，体现在以下四点。

（1）内置执行器。

Generator 函数的执行必须靠执行器，所以才有了co模块，而async函数自带执行器。也就是说，async函数的执行，与普通函数一模一样，只要一行。


上面的代码调用了asyncReadFile函数，然后它就会自动执行，输出最后结果。


（2）更好的语义。

async和await，比起星号和yield，语义更清楚了。async表示函数里有异步操作，await表示紧跟在后面的表达式需要等待结果。


（3）更广的适用性。

co模块约定，yield命令后面只能是 Thunk 函数或 Promise 对象，而async函数的await命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时等同于同步操作）。

（4）返回值是 Promise。

async函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了。你可以用then方法指定下一步的操作。

进一步说，async函数完全可以看作多个异步操作，包装成的一个 Promise 对象，而await命令就是内部then命令的语法糖。

基本用法
async函数返回一个 Promise 对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句


语法
async函数的语法规则总体上比较简单，难点是错误处理机制。


返回 Promise 对象
async函数返回一个 Promise 对象。

async函数内部return语句返回的值，会成为then方法回调函数的参数。

async函数内部抛出错误，会导致返回的 Promise 对象变为reject状态。抛出的错误对象会被catch方法回调函数接收到。

Promise 对象的状态变化 § ?
async函数返回的 Promise 对象，必须等到内部所有await命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到return语句或者抛出错误。也就是说，只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数。

await 命令
正常情况下，await命令后面是一个 Promise 对象。如果不是，会被转成一个立即resolve的 Promise 对象。


await命令后面的 Promise 对象如果变为reject状态，则reject的参数会被catch方法的回调函数接收到。

有时，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个await放在try...catch结构里面，这样不管这个异步操作是否成功，第二个await都会执行。

另一种方法是await后面的 Promise 对象再跟一个catch方法，处理前面可能出现的错误。

使用注意点
第一点，前面已经说过，await命令后面的Promise对象，运行结果可能是rejected，所以最好把await命令放在try...catch代码块中。

第二点，多个await命令后面的异步操作，如果不存在继发关系，最好让它们同时触发。


第三点，await命令只能用在async函数之中，如果用在普通函数，就会报错。


第十九课clsss

注意，定义“类”的方法的时候，前面不需要加上function这个关键字，直接把函数定义放进去了就可以了。另外，方法之间不需要逗号分隔，加了会报错。


类的数据类型就是函数，类本身就指向构造函数。

使用的时候，也是直接对类使用new命令，跟构造函数的用法完全一致。

构造函数的prototype属性，在 ES6 的“类”上面继续存在。事实上，类的所有方法都定义在类的prototype属性上面。

由于类的方法都定义在prototype对象上面，所以类的新方法可以添加在prototype对象上面。Object.assign方法可以很方便地一次向类添加多个方法。


prototype对象的constructor属性，直接指向“类”的本身，这与 ES5 的行为是一致的。


类的内部所有定义的方法，都是不可枚举的（non-enumerable）。

类的属性名，可以采用表达式。


类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。


constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加。

类必须使用new调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。


生成类的实例对象的写法，与 ES5 完全一样，也是使用new命令。前面说过，如果忘记加上new，像函数那样调用Class，将会报错。


与 ES5 一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。


与函数一样，类也可以使用表达式的形式定

采用 Class 表达式，可以写出立即执行的 Class。

类不存在变量提升（hoist），这一点与 ES5 完全不同

ES6 不会把类的声明提升到代码头部。这种规定的原因与下文要提到的继承有关，必须保证子类在父类之后定义。


私有方法是常见需求，但 ES6 不提供，只能通过变通方法模拟实现
一种做法是在命名上加以区别。
（_bar方法前面的下划线，表示这是一个只限于内部使用的私有方法。）

另一种方法就是索性将私有方法移出模块，因为模块内部的所有方法都是对外可见的。

还有一种方法是利用Symbol值的唯一性，将私有方法的名字命名为一个Symbol值。


私有属性的提案
与私有方法一样，ES6 不支持私有属性。目前，有一个提案，为class加了私有属性。方法是在属性名之前，使用#表示。

私有属性可以指定初始值，在构造函数执行时进行初始化。

私有属性也可以设置 getter 和 setter 方法

类的方法内部如果含有this，它默认指向类的实例。

一个比较简单的解决方法是，在构造方法中绑定this，这样就不会找不到print方法了。
另一种解决方法是使用箭头函数。
还有一种解决方法是使用Proxy，获取方法的时候，自动绑定this

name属性总是返回紧跟在class关键字后面的类名。

如果某个方法之前加上星号（*），就表示该方法是一个 Generator 函数。


如果某个方法之前加上星号（*），就表示该方法是一个 Generator 函数。


注意，如果静态方法包含this关键字，这个this指的是类，而不是实例。

静态方法可以与非静态方法重名。
父类的静态方法，可以被子类继承。

静态方法也是可以从super对象上调用的。父类的静态方法，可以被子类继承。

静态属性指的是 Class 本身的属性，即Class.propName，而不是定义在实例对象（this）上的属性。


类的实例属性可以用等式，写入类的定义之中。

类的静态属性只要在上面的实例属性写法前面，加上static关键字就可以了。

为了可读性的目的，对于那些在constructor里面已经定义的实例属性，新写法允许直接列出。


ES6 为new命令引入了一个new.target属性，该属性一般用在构造函数之中，返回new命令作用于的那个构造函数。如果构造函数不是通过new命令调用的，new.target会返回undefined，因此这个属性可以用来确定构造函数是怎么调用的。

Class 内部调用new.target，返回当前 Class

子类继承父类时，new.target会返回子类。


第二是课class的继承

Class 可以通过extends关键字实现继承，

super关键字，它在这里表示父类的构造函数，用来新建父类的this对象。

子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。


另一个需要注意的地方是，在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错。这是因为子类实例的构建，是基于对父类实例加工，只有super方法才能返回父类实例。

Object.getPrototypeOf方法可以用来从子类上获取父类

此，可以使用这个方法判断，一个类是否继承了另一个类。

super这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。

第一种情况，super作为函数调用时，代表父类的构造函数。ES6 要求，子类的构造函数必须执行一次super函数。

作为函数时，super()只能用在子类的构造函数之中，用在其他地方就会报错。

这里需要注意，由于super指向父类的原型对象，所以定义在父类实例上的方法或属性，是无法通过super调用的。

ES6 规定，通过super调用父类的方法时，方法内部的this指向当前的子类实例。

由于this指向子类实例，所以如果通过super对某个属性赋值，这时super就是this，赋值的属性会变成子类实例的属性。

如果super作为对象，用在静态方法之中，这时super将指向父类，而不是父类的原型对象。


注意，使用super的时候，必须显式指定是作为函数、还是作为对象使用，否则会报错。


最后，由于对象总是继承其他对象的，所以可以在任意一个对象中，使用super关键字。


（1）子类的__proto__属性，表示构造函数的继承，总是指向父类。

（2）子类prototype属性的__proto__属性，表示方法的继承，总是指向父类的prototype属性。

extends关键字后面可以跟多种类型的值。


ECMAScript 的原生构造函数大致有下面这些。

Boolean()
Number()
String()
Array()
Date()
Function()
RegExp()
Error()
Object()

第二十一课修饰器

许多面向对象的语言都有修饰器（Decorator）函数，用来修改类的行为。

也就是说，修饰器是一个对类进行处理的函数。修饰器函数的第一个参数，就是所要修饰的目标类。

第22课 Module
ES6 可以在编译时就完成模块加载，

模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能


ES6 将其视为一个模块，里面用export命令对外部输出了三个变量。


使用大括号指定所要输出的一组变量。它与前一种写法（直接放置在var语句前）是等价的，但是应该优先考虑使用这种写法。因为这样就可以在脚本尾部，一眼看清楚输出了哪些变量。

export命令除了输出变量，还可以输出函数或类（class）


通常情况下，export输出的变量就是本来的名字，但是可以使用as关键字重命名。


另外，export语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值

export命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错，下一节的import命令也是如此。这是因为处于条件代码块之中，就没法做静态优化了，违背了 ES6 模块的设计初衷。

使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。


import命令接受一对大括号，里面指定要从其他模块导入的变量名。大括号里面的变量名，必须与被导入模块（profile.js）对外接口的名称相同。


如果想为输入的变量重新取一个名字，import命令要使用as关键字，将输入的变量重命名。

import命令输入的变量都是只读的，因为它的本质是输入接口。也就是说，不允许在加载模块的脚本里面，改写接口。


建议凡是输入的变量，都当作完全只读，轻易不要改变它的属性。

import后面的from指定模块文件的位置，可以是相对路径，也可以是绝对路径，.js后缀可以省略。如果只是模块名，不带有路径，那么必须有配置文件，告诉 JavaScript 引擎该模块的位置。

注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。


因为import的执行早于foo的调用。这种行为的本质是，import命令是编译阶段执行的，在代码运行之前。

由于import是静态执行，所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构。

import语句会执行所加载的模块，因此可以有下面的写法。
import 'lodash';

如果多次重复执行同一句import语句，那么只会执行一次，而不会执行多次。

除了指定加载某个输出值，还可以使用整体加载，即用星号（*）指定一个对象，所有输出值都加载在这个对象上面。


注意，模块整体加载所在的那个对象（上例是circle），应该是可以静态分析的，所以不允许运行时改变。下面的写法都是不允许的。


export default命令，为模块指定默认输出。

其他模块加载该模块时，import命令可以为该匿名函数指定任意名字。

需要注意的是，这时import命令后面，不使用大括号。

export default命令用在非匿名函数前，也是可以的

const声明的常量只在当前代码块有效。


import命令会被 JavaScript 引擎静态分析，先于模块内的其他语句执行（import命令叫做”连接“ binding 其实更合适）。

建议引入import()函数，完成动态加载。

import()返回一个 Promise 对象。

import()函数可以用在任何地方，不仅仅是模块，非模块的脚本也可以使用。它是运行时执行，也就是说，什么时候运行到这一句，就会加载指定的模块。另外，import()函数与所加载的模块没有静态连接关系，这点也是与import语句不相同。

import()类似于 Node 的require方法，区别主要是前者是异步加载，后者是同步加载。import()的浏览器实现，类似于下面的写法。

import()可以在需要的时候，再加载某个模块。

import()可以放在if代码块，根据不同的情况，加载不同的模块。

import()允许模块路径动态生成。

import()加载模块成功以后，这个模块会作为一个对象，当作then方法的参数。因此，可以使用对象解构赋值的语法，获取输出接口。


第二十三课Module

defer与async的区别是：defer要等到整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），才会执行；async一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。一句话，defer是“渲染完再执行”，async是“下载完就执行”。另外，如果有多个defer脚本，会按照它们在页面出现的顺序加载，而多个async脚本是不能保证加载顺序的。

浏览器对于带有type="module"的<script>，都是异步加载，不会造成堵塞浏览器，即等到整个页面渲染完，再执行模块脚本，等同于打开了<script>标签的defer属性。

Node 的import命令是异步加载，这一点与浏览器的处理方法相同。


CommonJS 模块的输出都定义在module.exports这个属性上面。Node 的import命令加载 CommonJS 模块，Node 会自动将module.exports属性，当作模块的默认输出，即等同于export default xxx。

CommonJS 模块加载 ES6 模块，不能使用require命令，而要使用import()函数。ES6 模块的所有输出接口，会成为输入对象的属性。


