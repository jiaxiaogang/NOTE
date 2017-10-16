```objective-c
/** *  MARK:--------------------DB-------------------- */+(void)initialize{    [self setUserCalculateForCN:@"content"];//这里不写,进不到userGetValueForModel方法;    [self removePropertyWithColumnName:@"pointer"];} -(id)userGetValueForModel:(LKDBProperty *)property{    if([property.propertyName isEqualToString:@"content"]){        NSCoder *enCoder = [[NSCoder alloc] init];        [self encodeWithCoder:enCoder];        return enCoder;    }    return [super userGetValueForModel:property];} -(void)userSetValueForModel:(LKDBProperty *)property value:(id)value{    [super userSetValueForModel:property value:value];} +(BOOL) isContainParent{    return true;} +(BOOL) isContainSelf{    return true;}   /** *  MARK:--------------------联表查询-------------------- */+(void)initialize{    [super initialize];    [self setUserCalculateForCN:@"mindValue"];} -(id)userGetValueForModel:(LKDBProperty *)property{    if([property.sqlColumnName isEqualToString:@"mindValue"] && self.mindValue != nil){        [AIMindValue insertToDB:self.mindValue];        return @(self.mindValue.rowid);    }    return nil;} -(void)userSetValueForModel:(LKDBProperty *)property value:(id)value {    if([property.sqlColumnName isEqualToString:@"mindValue"]) {        self.mindValue = [AIMindValue ai_searchSingleWithRowId:[STRTOOK(value) intValue]];    }} //查询AIMindValue *searchMV = [[AIMindValue searchWithWhere:[DBUtils sqlWhereDic_K:@"type" V:@(MindType_Hunger)]] lastObject];            NSLog(@"");            NSMutableArray *searchMem = [AIMemory searchWithWhere:[DBUtils sqlWhereDic_K:@"mindValue" V:@(searchMV.rowid)]];            NSLog(@""); 
```









