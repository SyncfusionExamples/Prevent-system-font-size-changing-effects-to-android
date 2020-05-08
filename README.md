# Prevent-system-font-size-changing-effects-to-android

This article explains how to restrict the system font size changes effects to SfAutoComplete control in Xamarin.Forms Android platform as per in below code snippet

**[XAML]**

Let’s have an SfAutoComplete control with FontSize of 20.
``` 
<StackLayout Margin="0,50,10,10">
        <autocomplete:SfAutoComplete HeightRequest="60" Text="Font-20" TextSize="20"/>
 </StackLayout>
 ```

**[C#]**

In the Xamarin.Forms Android MainActivity.cs, override the Resources and set the configuration to default to restrict the font size effect on application. Resources.UpdateConfiguration() has been deprecated in API 25. So CreateConfigurationContext is used for APl level greater than 25.

```
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
        public override Resources Resources
        {
                Resources resource = base.Resources;
                Configuration configuration = new Configuration();
                configuration.SetToDefaults();
                if (Build.VERSION.SdkInt >= Build.VERSION_CODES.NMr1)
                {
                    return CreateConfigurationContext(configuration).Resources;
                }
                else
                {
                    resource.UpdateConfiguration(configuration, resource.DisplayMetrics);
                    return resource;
                }        
        }
    …
}
```
**Output**

*Before applying the changes*

Entry with font size of 20

![Entry with font size of 20
](https://github.com/SyncfusionExamples/Prevent-system-font-size-changing-effects-to-android/blob/master/FontSample/Screenshots/Entry_FontSize_20.png)

Change the system font size

![Change the system font size
](https://github.com/SyncfusionExamples/Prevent-system-font-size-changing-effects-to-android/blob/master/FontSample/Screenshots/System-Font-Size-Changes.png)

Entry looks with huge font size

![Entry looks with huge font size](https://github.com/SyncfusionExamples/Prevent-system-font-size-changing-effects-to-android/blob/master/FontSample/Screenshots/Changes-in-font-size.png)


*After applying the changes, it keeps in same*

![Desired output](https://github.com/SyncfusionExamples/Prevent-system-font-size-changing-effects-to-android/blob/master/FontSample/Screenshots/Desired_Output.png)

