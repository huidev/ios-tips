## json-framework的使用

## 配置 以4.01为准

````objc

1:手动：下载源码后将文件夹中src－main－objc中代码考到项目中
2:自动：pod 'SBJson', '~> 4.0.1'

````

## 使用

````objc

    //1:设置代码执行block和初始化工具
  
    //初始化读取类
	SBJson4Writer *writer = [[SBJson4Writer alloc] init];
	//初始化block
    SBJson4ValueBlock block = ^(id obj, BOOL *stop) {
       //处理json数据和类型的地方

    };
    //初始化解析类
    SBJson4Parser *parser =  [SBJson4Parser parserWithBlock:block allowMultiRoot:NO unwrapRootArray:NO errorHandler:nil];
    //执行解析
	[parser parse:[jsonString dataUsingEncoding:NSUTF8StringEncoding]];

````

## 解析例子

````objc

－－－－－－－－－解析为string
 SBJson4Writer *writer = [[SBJson4Writer alloc] init];
//方式1:通过nsdata转string
id data = [writer dataWithObject:obj];
NSString *str = [[NSString alloc]initWithData:data encoding:(NSUTF8StringEncoding)];
//方式2，直接使用[writer stringWithObject:obj]
NSLog(@"Found: %@", [writer stringWithObject:obj]);

－－－－－－－－－解析为dict
SBJson4Writer *writer = [[SBJson4Writer alloc] init];
//解析为字典
id data = [writer dataWithObject:obj];
NSDictionary *dic = [NSJSONSerialization
                      JSONObjectWithData:data
                      options:kNilOptions
                      error:nil];

//解析字典下的内容
NSDictionary *china = [dic objectForKey:@"中国"];
NSLog(@"key=北京%@",[china objectForKey:@"北京"]);

－－－－－－－－－解析为array

－－－－－－－－－解析为对象

 NSString *jsonString=@"{\"中国\":{ \"北京\":{\"北京1\":1,\"北京2\":2,\"北京3\":3},  \"上海\":{\"上海1\":4,\"上海2\":5,\"上海3\":6},\"广州\":{\"广州1\":7,\"广州2\":8,\"广州3\":9}}}";

    SBJson4ValueBlock block = ^(id obj, BOOL *stop) {
        SBJson4Writer *writer = [[SBJson4Writer alloc] init];
        id data = [writer dataWithObject:obj];
        NSLog(@"Found: %@", [writer stringWithObject:obj]);
 
      // NSMutableDictionary *dic = [NSMutableDictionary
        NSString *str = [[NSString alloc]initWithData:data encoding:(NSUTF8StringEncoding)];
        //NSLog(@"Found: %@",str);

    };

````

