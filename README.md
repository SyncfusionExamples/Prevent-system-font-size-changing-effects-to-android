# Prevent-system-font-size-changing-effects-to-android

This article explains how to restrict the system font size changes effects to Entry control in Xamarin.Forms Android platform as per in below code snippet

**[XAML]**

Let’s have an Entry control with FontSize of 20 
```
<StackLayout>
        <Entry Text="Font Size" FontSize="20"
           HorizontalOptions="Center"
           VerticalOptions="CenterAndExpand" />
</StackLayout> 
```

**[C#]**

In the Xamarin.Forms Android MainActivity.cs, add the below code to restrict the font size effect on application.

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

!()[FontSample/Screenshots/Changes-in-font-size.png)

Change the system font size

Entry looks with huge font size

*After applying the changes, it keeps in same*



