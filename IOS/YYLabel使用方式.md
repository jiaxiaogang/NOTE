- [ ] <font color="red" size="5">YYLabel</font>

```java

//1,newYYLabel
YYLabel *openLab = [[YYLabel alloc]init];
[openLab setSize:CGSizeMake(ScreenWidth - 32, MAXFLOAT)];
openLab.numberOfLines = 0;

//2,NSMutableAttributedString
NSMutableAttributedString *mStr = [NSAttributedString createMStr:desc
                                                        withFont:[ENUntil defaultFontOfSize:14 * FontScale]
                                                  withLineHeight:19
                                                   withTextColor:[UIColor redColor]];

//3,为自定义View留空间
UIView *replaceView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, 188, 188)];
NSMutableAttributedString *attachText = [NSMutableAttributedString
                                         yy_attachmentStringWithContent:replaceView
                                         contentMode:UIViewContentModeCenter
                                         attachmentSize:replaceView.size
                                         alignToFont:[ENUntil defaultFontOfSize:19]
                                         alignment:YYTextVerticalAlignmentCenter];
[mStr insertAttributedString:attachText atIndex:0];

//4,插入自定义View
UIView *insertView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, 188, 188)];
[self.descView addSubview:insertView];

//5,setAttributedText
[openLab setAttributedText:mStr];

//6,其它:
CGFloat openLabH = [self.openLab sizeThatFits:CGSizeMake(ScreenWidth - 32, CGFLOAT_MAX)].height + 1;//取高度
[self.openLab setFrame:CGRectMake(0, 0, ScreenWidth - 32, openLabH )];//设置高度
    
```
    

- [ ] <font color="red" size="5">YYLabel贝塞尔的代码如下:</font>

```
//贝塞尔的代码如下:
NSMutableAttributedString *title = [[NSMutableAttributedString alloc] initWithString:@"asdfasdf"];

YYLabel *tempLab = [[YYLabel alloc]init];
[tempLab setSize:CGSizeMake(ScreenWidth - 32, MAXFLOAT)];
[tempLab setAttributedText:brief];
tempLab.numberOfLines = 0;

//贝赛尔;图片leftMargin10;bottomMargin6;
UIBezierPath *path = [UIBezierPath bezierPathWithRect:CGRectMake(ScreenWidth - 16 - 16 - 20, 0, 20, 5)];
tempLab.exclusionPaths = @[path];
```
