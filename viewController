//
//  ViewController.m
//  pictureTest
//
//  Created by 007 on 15/10/30.
//  Copyright © 2015年 闫莎. All rights reserved.
//

#import "ViewController.h"

#define NavigationBarHeight 64.0f
#define  ImageHeight 200.0f
@interface ViewController ()<UITableViewDataSource,UITableViewDelegate,UINavigationControllerDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    //  设置导航栏透明度为0
    self.navigationController.navigationBar.backgroundColor = [UIColor clearColor];
    [self.navigationController.navigationBar setTranslucent:YES];
    self.navigationController.view.backgroundColor = [UIColor clearColor];
    [self.navigationController.navigationBar setBackgroundImage:[[UIImage alloc] init] forBarMetrics:UIBarMetricsDefault];
    self.navigationController.navigationBar.shadowImage = [[UIImage alloc] init];
    self.navigationController.navigationBar.backgroundColor = [UIColor clearColor];
    self.navigationController.delegate=self;
    //2.初始化_tableView
    self.listTableView = [[UITableView alloc]initWithFrame:CGRectMake(0, -64, self.view.frame.size.width, self.view.frame.size.height+64) style:UITableViewStylePlain];
    //3.设置代理，头文件也要包含 UITableViewDelegate,UITableViewDataSource
    self.listTableView.delegate = self;
    self.listTableView.dataSource = self;
    //4.设置contentInset属性（上左下右 的值）
    self.listTableView.contentInset = UIEdgeInsetsMake(ImageHeight, 0, 0, 0);
    //5.添加_tableView
    [self.view addSubview:self.listTableView];
    _zoomImageView=[[UIImageView alloc]initWithFrame:CGRectMake(0, -ImageHeight, self.view.frame.size.width, ImageHeight)];
    _zoomImageView.image=[UIImage imageNamed:@"aa.jpg"];
   _zoomImageView.contentMode=UIViewContentModeScaleAspectFill;//不设置contentMode只会竖向拉伸
    [self.listTableView addSubview:_zoomImageView];
    _zoomImageView.autoresizesSubviews=YES;

}

- (void)scrollViewDidScroll:(UIScrollView *)scrollView{
    
    CGFloat y = scrollView.contentOffset.y+NavigationBarHeight;//根据实际选择加不加上NavigationBarHight（44、64 或者没有导航条）
    if (y < -ImageHeight) {
        CGRect frame = _zoomImageView.frame;
        frame.origin.y = y;
        frame.size.height =  -y;//contentMode = UIViewContentModeScaleAspectFill时，高度改变宽度也跟着改变
        _zoomImageView.frame = frame;
    }
    //  随着表格滑动设置导航栏的颜色
    UIColor *color=[UIColor greenColor];
    CGFloat offset=scrollView.contentOffset.y;
    if (offset<0) {
        self.navigationController.navigationBar.backgroundColor = [color colorWithAlphaComponent:0];
    }else {
        CGFloat alpha=1-((64-offset)/64);
        if (alpha>0.4){
            alpha=0.4;
        }
            self.navigationController.navigationBar.backgroundColor=[color colorWithAlphaComponent:alpha];
            [[UINavigationBar appearance]setBarTintColor:color];
        
    }
}

#pragma mark - Table view data source

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
{
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return 20;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    UITableViewCell *cell=[tableView dequeueReusableCellWithIdentifier:@"这个自己命名"];
    if(cell==nil){
        cell=[[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"这个自己命名"];
        cell.selectionStyle = UITableViewCellSelectionStyleNone;
        cell.separatorInset=UIEdgeInsetsZero;
        cell.clipsToBounds = YES;
    }
    
    cell.textLabel.text = [NSString stringWithFormat:@"第 %ld 行",indexPath.row];
    
    return cell;
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end
