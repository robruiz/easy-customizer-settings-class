# Easy Customizer Settings Class
Create and manage theme settings in the WordPress Customizer using a structured array.
This is perfect for themes and will likely get included into WP Rig.

## How To Use:
- Include the class in your theme's functions.php
- Create your args array and pass into class when instantiated, like this:
```
$settings_config = array(
    'theme_name' => 'YourTheme',
    'settings_id' => 'yourTheme_theme',
    'sections' => array(
        array (
            'id' => 'global',
            'title' => __( 'YourTheme Settings', 'yourTheme' ),
            'priority' => 30
        )
    ),
    'settings' => array(
        array(
            'id' => 'ga_id',
            'label' => 'Google Analytics ID',
            'section' => 'global',
            'refresh' => false
        ),
        array(
            'id' => 'enable_fontawesome',
            'label' => 'Enable Font Awesome Icons',
            'type' => 'checkbox',
            'section' => 'global',
            'refresh' => false
        )
    )
);

$theme_settings = new EZ_Customizer_Settings($settings_config);

```
- That's it! It's that EZ!

## How it works:
The structure of the array attempts to follow the core function args in WordPress
as much as possible, however, some liberties were taken to improve simplicity

### Array structure details
- **theme_name**: The name of your theme (without spaces - like an ID)
- **settings_id**: Unique ID for these settings (for storage in the DB)(I might make this optional in the future)
- **sections**: Define each new section to be added to the customizer. We lumped in id for simplicity. 'title' allows for localization
  
  - Refer to [WP Codex Docs](https://developer.wordpress.org/reference/classes/wp_customize_section/__construct/) for all args
- **settings**: Each setting is it's own array in this array of settings. We tried to combine the args for settings and controls as much as possible to keep this as simple as possible. For the most part, all args from [this WP Codex function](https://developer.wordpress.org/reference/classes/wp_customize_setting/__construct/) apply. Also All control args can be passed in, [view Codex docs for controls](https://developer.wordpress.org/reference/classes/wp_customize_control/__construct/) for more details on how those work. We changed 'transport' to 'refresh' because it makes more sense
  - **type**: (optional) All base core types are currently supported. Type is optional, if not included, a basic text field is assumed. The following more complex types are also supported:
    - Basic Types include: 'text', 'checkbox', 'textarea', 'radio', 'select', and 'dropdown-pages'. Additional input types such as 'email', 'url', 'number', 'hidden', and 'date' are supported implicitly.
    - **color** - Color Picker
    - **date** - Data/Time Picker
    - **media** - Image/Attachment Selection
If you have any ideas for improvement, please submit an issue or a PR. Thanks!