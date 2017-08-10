# swift-UITextField
各种属性设置

        //1.文本框的创建，有如下几个样式：
//        UITextBorderStyle.none：无边框
//        UITextBorderStyle.line：直线边框
//        UITextBorderStyle.roundedRect：圆角矩形边框
//        UITextBorderStyle.bezel：边线+阴影
        let textField = UITextField(frame:CGRect(x:10, y:60, width:200, height:30))
        //设置边框样式为圆角矩形
        textField.borderStyle = UITextBorderStyle.roundedRect
        //字体属性设置
        textField.textColor = UIColor.black
        textField.font = UIFont(name:"GillSans",size:15)
        textField.textAlignment = NSTextAlignment.left
        /** 垂直对齐 **/
        //textField.contentVerticalAlignment = .top  //垂直向上对齐
        textField.contentVerticalAlignment = .center  //垂直居中对齐
        //textField.contentVerticalAlignment = .bottom  //垂直向下对齐
        //文本框提示文字
        textField.placeholder = "请输入文字"
        //明文显示
        textField.isSecureTextEntry = false
        //光标颜色
        textField.tintColor = UIColor.green
        //文字大小超过文本框长度时自动缩小字号，而不是隐藏显示省略号
        //textField.adjustsFontSizeToFitWidth = true//当文字超出文本框宽度时，自动调整文字大小
        //textField.minimumFontSize = 12//最小可缩小的字号
        //是否可操作
        textField.isEnabled = true
        textField.isUserInteractionEnabled = true
        //背景图片设置
        textField.borderStyle = .none//先要去除边框样式,否则无效
        textField.background = UIImage(named:"daohanglan_touming@2x")
        //清除按钮（输入框内右侧小叉）
        textField.clearButtonMode = .whileEditing
        //设置文本框关联的键盘类型
//        Default：系统默认的虚拟键盘
//        ASCII Capable：显示英文字母的虚拟键盘
//        Numbers and Punctuation：显示数字和标点的虚拟键盘
//        URL：显示便于输入url网址的虚拟键盘
//        Number Pad：显示便于输入数字的虚拟键盘
//        Phone Pad：显示便于拨号呼叫的虚拟键盘
//        Name Phone Pad：显示便于聊天拨号的虚拟键盘
//        Email Address：显示便于输入Email的虚拟键盘
//        Decimal Pad：显示用于输入数字和小数点的虚拟键盘
//        Twitter：显示方便些Twitter的虚拟键盘
//        Web Search：显示便于在网页上书写的虚拟键盘
        textField.keyboardType = .default
        //使文本框在界面打开时就获取焦点，并弹出输入键盘(第一响应着)
        textField.becomeFirstResponder()
        //使文本框失去焦点，并收回键盘
        //textField.resignFirstResponder()
        //设置键盘return键的样式
//        textField.returnKeyType = UIReturnKeyType.done //表示完成输入
//        textField.returnKeyType = UIReturnKeyType.go //表示完成输入，同时会跳到另一页
//        textField.returnKeyType = UIReturnKeyType.search //表示搜索
//        textField.returnKeyType = UIReturnKeyType.join //表示注册用户或添加数据
//        textField.returnKeyType = UIReturnKeyType.next //表示继续下一步
//        textField.returnKeyType = UIReturnKeyType.send //表示发送
        textField.returnKeyType = .send
        //设置代理
        textField.delegate = self
        
        // 自定义输入源控件 
//        let inputview = UIButton(frame: CGRect(x:0.0, y:0.0, width:self.view.bounds.width, height:100.0))
//         inputview.setImage(UIImage(named: "daohanglan_touming@2x"), for: UIControlState.normal)
//         inputview.backgroundColor = UIColor.lightGray
//         inputview.addTarget(self, action: Selector(click:), for: UIControlEvents.touchUpInside)
//         textField.inputView = inputview
        // 自定义输入源控件副视图
        let accessoryview = UIView(frame: CGRect(x:0.0, y:0.0, width:self.view.frame.size.width, height:40.0))
        accessoryview.backgroundColor = UIColor.green
        let accessoryLeft = UIButton(frame: CGRect(x:10.0, y:10.0, width:60.0, height:20.0))
        accessoryview.addSubview(accessoryLeft)
        accessoryLeft.setTitle("取消", for: UIControlState.normal)
        accessoryLeft.backgroundColor = UIColor.orange
        accessoryLeft.addTarget(self, action: #selector(leftClick), for: UIControlEvents.touchUpInside)
        let accessoryRight = UIButton(frame: CGRect(x:(accessoryview.bounds.width - 10.0 - 60.0), y:10.0, width:60.0, height:20.0))
        accessoryview.addSubview(accessoryRight)
        accessoryRight.setTitle("确定", for: UIControlState.normal)
        accessoryRight.backgroundColor = UIColor.orange
        accessoryRight.addTarget(self, action: #selector(rightClick), for: UIControlEvents.touchUpInside)
        textField.inputAccessoryView = accessoryview
        
        // 发通知-输入改变
        NotificationCenter.default.addObserver(self, selector: #selector(textFiledEditChanged), name: NSNotification.Name.UITextFieldTextDidChange, object: textField)
        
        
        self.view.addSubview(textField)
    }
    //键盘return按钮点击事件
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        //收起键盘
        //textField.resignFirstResponder()
        self.view .endEditing(true)
        
        print(textField.text!)
        return true;
    }
    
    // 自定义输入源控件时响应事件
    // MARK: - click
    func click(button:UIButton)
    {
        self.view.endEditing(true)
    }
    //MARK: - left/right click
    func leftClick(button:UIButton)
    {
        print("取消")
    }
    
    func rightClick(button:UIButton)
    {
        self.view.endEditing(true)
        print("确定")  
    }
    // 通知响应方法-限制输入长度
    // MARK: - 通知响应方法
    func textFiledEditChanged(notification:NSNotification)
    {
        let textField:UITextField! = notification.object as! UITextField
        if (textField != nil)
        {
            let text:String! = textField.text
            let length = text.characters.count
            if (length > 20)
            {
            }
        }
    }
    // 代理方法
    // MARK: - UITextFieldDelegate
    func textFieldShouldBeginEditing(_ textField: UITextField) -> Bool {
        
        print("1 textFieldShouldBeginEditing")
        
        return true
    }
    func textFieldDidBeginEditing(_ textField: UITextField) {
        print("2 textFieldDidBeginEditing")
    }
    
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        print("3 textField")
        
        return true
    }
    func textFieldShouldEndEditing(_ textField: UITextField) -> Bool {
        print("4 textFieldShouldEndEditing")
        print("text：\(String(describing: textField.text)) length = \(String(describing: textField.text?.characters.count))")
        return true
    }
    
    func textFieldDidEndEditing(_ textField: UITextField) {
        print("5 textFieldDidEndEditing")
    }
    
    func textFieldShouldClear(_ textField: UITextField) -> Bool {
        
        print("6 textFieldShouldClear")
        return true
    }
    
    func textFieldShouldReturn(textField: UITextField) -> Bool {
        // 结束编辑
        textField.resignFirstResponder()
        print("7 textFieldShouldReturn")
        return true
    }


![](https://github.com/jixiang0903/swift-UITextField/blob/master/WechatIMG66.jpeg)
