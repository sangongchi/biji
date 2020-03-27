### 1.bcrypt

---

1. 安装 `npm install bcrypt`

2. 使用

    ```js
    // 导入模块
    const bcrypt = require('bcrypt');
    // 加密的幂次
    const saltRounds = 10; // 默认 10
    // 明文密码
    const myPlaintextPassword = 'password';
    
    // [方式一] 将明文密码字符串加密
    bcrypt.genSalt(saltRounds, function(err, salt) {
        bcrypt.hash(myPlaintextPassword, salt, function(err, hash) {
            // Store hash in your password DB.
        });
    });
    // [方式二]
    bcrypt.hash(myPlaintextPassword, saltRounds, function(err, hash) {
      // Store hash in your password DB.
    });
    
    // 校验用户密码
    bcrypt.compare(myPlaintextPassword, hash, function(err, res) {
        // res == true
    });
    ```

    

