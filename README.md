# How to customize TreeView ItemTemplate based on the node in Xamarin.Forms (SfTreeView)

You can customize TextColor and FontSize of [SfTreeView](https://help.syncfusion.com/xamarin/treeview/overview?) node based on the node level using [Converters](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters) in Xamarin.Forms.

You can also refer the following article.

https://www.syncfusion.com/kb/11393/how-to-customize-treeview-node-based-on-the-node-level-in-xamarin-forms-sftreeview

**XAML**

Binding the [Level](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfTreeView.XForms~Syncfusion.TreeView.Engine.TreeViewNode~Level.html?) property with converters in ItemTemplate.
``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:TreeViewXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.XForms.TreeView;assembly=Syncfusion.SfTreeView.XForms"
             x:Class="TreeViewXamarin.MainPage">
 
    <ContentPage.BindingContext>
        <local:FileManagerViewModel x:Name="viewModel"/>
    </ContentPage.BindingContext>
 
    <ContentPage.Resources>
        <ResourceDictionary>
            <local:TextColorConverter x:Key="TextColorConverter"/>
            <local:FontSizeConverter x:Key="FontSizeConverter"/>
        </ResourceDictionary>
    </ContentPage.Resources>
 
    <syncfusion:SfTreeView x:Name="treeView" ItemHeight="40" Indentation="15" ExpanderWidth="40" ChildPropertyName="SubFiles" ItemTemplateContextType="Node" 
                           AutoExpandMode="AllNodesExpanded" ItemsSource="{Binding ImageNodeInfo}" VerticalOptions="Center">
        <syncfusion:SfTreeView.ItemTemplate>
            <DataTemplate>
                <Grid x:Name="grid" RowSpacing="0" >
                    <Grid.RowDefinitions>
                        <RowDefinition Height="*" />
                        <RowDefinition Height="1" />
                    </Grid.RowDefinitions>
                    <Grid RowSpacing="0" Grid.Row="0">
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="40" />
                            <ColumnDefinition Width="*" />
                        </Grid.ColumnDefinitions>
                        <Grid Padding="5,5,5,5">
                            <Image Source="{Binding Content.ImageIcon}" VerticalOptions="Center" HorizontalOptions="Center" HeightRequest="35" WidthRequest="35"/>
                        </Grid>
                        <Grid Grid.Column="1" VerticalOptions="Center">
                            <Label LineBreakMode="NoWrap" Text="{Binding Content.ItemName}" VerticalTextAlignment="Center"
                                   TextColor="{Binding Level, Converter={x:StaticResource TextColorConverter}}"
                                   FontSize="{Binding Level, Converter={x:StaticResource FontSizeConverter}}">
                            </Label>
                        </Grid>
                    </Grid>
                    <StackLayout Grid.Row="1"/>
                </Grid>
            </DataTemplate>
        </syncfusion:SfTreeView.ItemTemplate>
    </syncfusion:SfTreeView>
 
</ContentPage>
```
**C#**

Converter to customize **TextColor** based on node level.
``` c#
namespace TreeViewXamarin
{
    public class TextColorConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            var level = (int)value;
            if (level == 0)
                return Color.Red;
            else if (level == 1)
                return Color.Blue;
            else
                return Color.Green;
        }
 
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```
**C#**

Converter to customize **FontSize** based on node level
``` c#
namespace TreeViewXamarin
{
    public class FontSizeConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            var level = (int)value;
            if (level == 0)
                return 20;
            else if (level == 1)
                return 17;
            else
                return 14;
        }
 
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```
**Output**

![NodeCsutomizationCoverter](https://github.com/SyncfusionExamples/customize-node-level-treeview-xamarin/blob/master/ScreenShots/NodeCsutomizationCoverter.png)
