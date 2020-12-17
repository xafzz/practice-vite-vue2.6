# Currying 柯里化

    之所以单独搞个分支出来，是因为确实不明白，绕来绕去绕晕了
    先将分支搞好，以后在拿出时间来慢慢研究

### 经典面试题
###### 不写下来我怕我忘了,写下来也别考我,我不会

#### 实现一个add方法，使计算结果能够满足如下预期：

    add(1)(2)(3) = 6;
    add(1, 2, 3)(4) = 10;
    add(1)(2)(3)(4)(5) = 15;

#### 实现方法

    function add() {
        // 第一次执行时，定义一个数组专门用来存储所有的参数
        var _args = Array.prototype.slice.call(arguments);
        
        // 在内部声明一个函数，利用闭包的特性保存_args并收集所有的参数值
        var _adder = function() {
            _args.push(...arguments);
            return _adder;
        };
        
        // 利用toString隐式转换的特性，当最后执行时隐式转换，并计算最终的值返回
        _adder.toString = function () {
            return _args.reduce(function (a, b) {
                return a + b;
            });
        }
        return _adder;
    }
