# YYModel研究

YYModel也必须手写容器类属性方法，可以参见说明文档中[YYModel](https://github.com/ibireme/YYModel)的容器类属性部分.

@class Shadow, Border, Attachment;

@interface Attributes
@property NSString *name;
@property NSArray *shadows; //Array<Shadow>
@property NSSet *borders; //Set<Border>
@property NSMutableDictionary *attachments; //Dict<NSString,Attachment>
@end

@implementation Attributes
// 返回容器类中的所需要存放的数据类型 (以 Class 或 Class Name 的形式)。
+ (NSDictionary *)modelContainerPropertyGenericClass {
    return @{@"shadows" : [Shadow class],
             @"borders" : Border.class,
             @"attachments" : @"Attachment" };
}
@end

然后同时也在取属性的时候遍历了父类的属性（这个是必须的，因为取属性是获取不到父类的属性的）