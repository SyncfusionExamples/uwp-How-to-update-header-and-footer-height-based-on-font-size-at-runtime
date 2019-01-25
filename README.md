# How-to-update-header-and-footer-height-based-on-font-size-at-runtime


This example demonstrates how to update header and footer height based on font size at runtime.

ListView allows you to resize the header and footer item size based on the change in font size of the label element at runtime by calling [RefreshListViewItem](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~RefreshListViewItem.html) method asynchronously when [SfListView.AutoFitMode](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~AutoFitMode.html) is Height.

You can refer [Syncfusion Xamarin.Forms ListView's item customization](https://help.syncfusion.com/xamarin/sflistview/item-size-customization#updating-the-header-and-footer-height-based-on-font-at-runtime) for more details.

```
<ContentPage xmlns:syncfusion="clr-namespace:Syncfusion.ListView.XForms;assembly=Syncfusion.SfListView.XForms">       
 <Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="50"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <Button Text="Change FontSize" Command="{Binding ResizeHeaderFooterCommand}" CommandParameter="{x:Reference listView}"/>
    <syncfusion:SfListView x:Name="listView" 
                ItemsSource="{Binding Contacts}"
                BackgroundColor="#FFE8E8EC"
                AutoFitMode="Height">
                <syncfusion:SfListView.HeaderTemplate>
                    <DataTemplate>
                        <ViewCell>
                            <Grid>
                                <Label Text="Contact Details"
                                       FontSize="{Binding BindingContext.FontSize, Source={x:Reference listView}}"/>
                            </Grid>
                        </ViewCell>
                    </DataTemplate>
                </syncfusion:SfListView.HeaderTemplate>
                <syncfusion:SfListView.FooterTemplate>
                    <DataTemplate>
                        <ViewCell>
                            <Grid >
                                <Label Text="Contacts Count" FontSize="{Binding BindingContext.FontSize, Source={x:Reference listView}}"/>
                                <Label Text="{Binding Contacts.Count}" FontSize="{Binding BindingContext.FontSize, Source={x:Reference listView}}"/>
                            </Grid>
                        </ViewCell>
                    </DataTemplate>
                </syncfusion:SfListView.FooterTemplate>
    </syncfusion:SfListView>                
</ContentPage>
```
Below code defines how ResizeHeaderFooterCommand used in viewmodel to change the header and footer height at runtime.

```
namespace SfListViewSample
{
    public class ContactsViewModel : INotifyPropertyChanged
    {
        public Command ResizeHeaderFooterCommand { get; set; }
        private double MaxPhone = 70;
        private double MinPhone = 20;
        private double MaxTablet = 100;
        private double MinTablet = 30;
        public ContactsViewModel()
        {
           ResizeHeaderFooterCommand = new Command(ResizeHeaderFooter);
        }
        private void ResizeHeaderFooter(object obj)
        {
            list = obj as SfListView;
            var maxFont = Device.Idiom == TargetIdiom.Phone ? MaxPhone : MaxTablet;
            var minFont = (Device.Idiom == TargetIdiom.Phone) ? MinPhone : MinTablet;
            if (FontSize >= maxFont)
            {
                FontSize = minFont;
            }
            else
            {
                FontSize += 10;
            }
            list.RefreshListViewItem(-1, -1, true);
        }
    }
}       

```

## Requirements to run the demo

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) or [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/).
* Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting

### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
