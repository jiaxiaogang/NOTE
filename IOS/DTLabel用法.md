## DTLabel用法

```java

#import "YouClass.h"
#import "DTCoreText.h"

@interface YouClass ()<DTAttributedTextContentViewDelegate>

@property (weak, nonatomic) IBOutlet DTAttributedLabel *dtDescLab;

@end
@implementation YouClass

-(id) init{
    self = [super init];
    if (self) {
        [self initView];
    }
    return self;
}

-(void) initView {
    //dtDescLab
    self.dtDescLab.delegate = self;
}

-(void) refreshDisplay{
    //正文
    [self.dtDescLab setSize:CGSizeMake(ScreenWidth - 32, MAXFLOAT)];
    [self.dtDescLab setAttributedString:[YouClass getDescMStr:self.dic]];
    CGFloat descLabH = [self.dtDescLab sizeThatFits:CGSizeZero].height;
}

/**
 *  MARK:--------------------method--------------------
 */
+(NSAttributedString*) getDescMStr:(NSDictionary*)data
{
    NSString *contentStr = LOCALIZE_STRING(NSSTRINGTOISVALID([data objectForKey:@"content"]));
    
    void (^callBackBlock)(DTHTMLElement*) = ^(DTHTMLElement *element) {
        //修改图片的显示尺寸及收集textAttachment
        for (DTHTMLElement *oneChildElement in element.childNodes){
            if (oneChildElement.displayStyle == DTHTMLElementDisplayStyleInline && oneChildElement.textAttachment && oneChildElement.textAttachment.displaySize.height >= 0.0 && [oneChildElement.textAttachment isKindOfClass:[DTImageTextAttachment class]]){
                CGSize bigSize = CGSizeMake(ScreenWidth - 32, ScreenHeight);
                oneChildElement.textAttachment.displaySize = bigSize;//可以改你的自定义View的大小
            }
        }
    };
    //8,设置css样式
    CGFloat lineHeight = floor( (CGFloat)21.0f / 16.0f*100) / 100;   //行距
    DTCSSStylesheet *defaultStyleSheet = [[DTCSSStylesheet alloc] initWithStyleBlock:[NSString stringWithFormat: @"<style type = \"text/css\">blockquote{}blockquote img{max-width:%fpx;}blockquote div{background:#dddddd;padding:20px 0px 15px 0px;}p{line-height:%f;font-size:%dpx }a{font-size:%dpx; }</style>",ScreenWidth - 32,lineHeight,16,16]];
    
    //9,创建options;
    NSMutableDictionary *options = [NSMutableDictionary dictionaryWithObjectsAndKeys:
                                    [NSNumber numberWithFloat:1.0], NSTextSizeMultiplierDocumentOption,	//
                                    [NSValue valueWithCGSize:CGSizeMake(ScreenWidth - 32, ScreenHeight)], DTMaxImageSize,//最大图片尺寸
                                    @"Heiti SC", DTDefaultFontFamily,                                   //默认字体//@"STHeitiSC-Light"
                                    @(FALSE),DTDefaultLinkDecoration,                                   //链接下划线
                                    @(0),DTDefaultFirstLineHeadIndent,                  //首行缩进
                                    UIColorWithRGBHex(0x0367B2),DTDefaultLinkColor,
                                    UIColorWithRGBHex(0x014B82), DTDefaultLinkHighlightColor,
                                    @(16),DTDefaultFontSize,
                                    callBackBlock, DTWillFlushBlockCallBack,
                                    defaultStyleSheet, DTDefaultStyleSheet,
                                    @(kCTTextAlignmentJustified),DTDefaultTextAlignment,
                                    [[ThemeManager shareInstance] getColorWithName:@"general_00a0"],DTDefaultTextColor, nil];
    //10,解析
    NSAttributedString *string = [[NSAttributedString alloc] initWithHTMLData:[contentStr dataUsingEncoding:NSUTF8StringEncoding] options:options documentAttributes:NULL];
    return string;
}

/**
 *  MARK:--------------------DTAttributedTextContentViewDelegate--------------------
 */
- (UIView *)attributedTextContentView:(DTAttributedTextContentView *)attributedTextContentView viewForAttributedString:(NSAttributedString *)string frame:(CGRect)frame
{
    NSDictionary *attributes = [string attributesAtIndex:0 effectiveRange:NULL];
    
    NSURL *URL = [attributes objectForKey:DTLinkAttribute];
    NSString *identifier = [attributes objectForKey:DTGUIDAttribute];
    
    DTLinkButton *button = [[DTLinkButton alloc] initWithFrame:frame];
    button.URL = URL;
    button.minimumHitSize = CGSizeMake(25, 25); // adjusts it's bounds so that button is always large enough
    button.GUID = identifier;
    
    // get image with normal link text
    UIImage *normalImage = [attributedTextContentView contentImageWithBounds:frame options:DTCoreTextLayoutFrameDrawingDefault];
    [button setImage:normalImage forState:UIControlStateNormal];
    
    // get image for highlighted link text
    UIImage *highlightImage = [attributedTextContentView contentImageWithBounds:frame options:DTCoreTextLayoutFrameDrawingDrawLinksHighlighted];
    [button setImage:highlightImage forState:UIControlStateHighlighted];
    
    //打开链接事件
    [button addTarget:self action:@selector(linkPushed:) forControlEvents:UIControlEventTouchUpInside];
    
    return button;
}

- (UIView *)attributedTextContentView:(DTAttributedTextContentView *)attributedTextContentView viewForAttachment:(DTTextAttachment *)attachment frame:(CGRect)frame
{
    if ([attachment isKindOfClass:[DTImageTextAttachment class]]){
        CGSize size = [DetailUtils getDetailLazyImgViewBigSize:frame.size withMaxSize:CGSizeMake(ScreenWidth - 32, ScreenHeight)];
        DTLazyImageView *attView = [[DTLazyImageView alloc] initWithFrame:CGRectMake(0, frame.origin.y, size.width, size.height)];
        attView.url = [NSURL youImgUrl这里自己填];
        [attView.layer setMasksToBounds:true];
        [attView.layer setCornerRadius:3];
        [attView addMaskWithUIColor:[[ThemeManager shareInstance] getColorWithName:@"image_mask"] withCornerRadius:3];
        return attView;
    }
    return [UIView new];
}

- (void)linkPushed:(DTLinkButton *)button
{
    NSURL *btnUrl = button.URL;
    //自定义链接处理
}



@end


```