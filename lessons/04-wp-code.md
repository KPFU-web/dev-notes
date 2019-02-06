# Создание шаблона для WordPress

[Основная документация](https://developer.wordpress.org/themes/getting-started/)
- плагин [Query monitor](https://wordpress.org/plugins/query-monitor/)

Две **обязательные** составляющие:
- index.php
- style.css

Заголовки в CSS - определяют данные шаблона/темы WP

```
/*
Theme Name: Имя темы
Theme URI: https://wordpress.org/themes/twentyseventeen/
Author: the WordPress team
Author URI: https://wordpress.org/
Description: Описание темы
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: twentyseventeen
Tags: one-column, two-columns
*/
```
# Файлы темы (Template Files)

- index.php
- style.css
- front-page.php
- home.php
- header.php
- singular.php
- single.php
- single-{post-type}.php
- archive.php
- archive-{post-type}.php
- page.php
- page-{slug}.php
- category.php
- tag.php
- search.php
- 404.php

Внутри файлов темы используются специальные функции темы

# Ключевые функции темы

- `get_header()` - подключение шапки
- `get_footer()` -подключение подвала
- `get_sidebar()` - подключение сайдбара
- `get_search_form()` - подключение формы поиска
- `get_template_part()` - подключение отдельного файла

# Цикл WordPress

Базовый механизм вывода информации в файлах шаблона.
Извлекает информацию о каждой записи WP из базы данных и выводит.
Все что заключено внутри выводится **в каждом посте**

```
<?php if ( have_posts() ) : ?>
    <?php while ( have_posts() ) : the_post(); ?>
        ... Display post content
    <?php endwhile; ?>
<?php endif; ?>
```

### Что может быть внутри
- `the_title()` – Заголовок поста или страницы
- `the_content()` – основное содержимое поста
- `the_excerpt()` – первый 55 слов поста либо то что идет до разделения через `Read More`
- `the_category()` – категория
- `the_time()` – время публикации .
- `the_author()` – автор
- `the_tags()` – теги


# Подключение стилей и скриптов

Стили
```
wp_enqueue_style( $handle, $src, $deps, $ver, $media );
```

```
wp_enqueue_style( 'style', get_stylesheet_uri() );
```

```
wp_enqueue_style( 'slider', get_template_directory_uri() . '/css/slider.css', array(), '1.1', 'all');
```

Скрипты
```
wp_enqueue_script( $handle, $src, $deps, $ver, $in_footer);
```


# Создание меню навигации

Регистрируем области в `functions.php`

```
function register_my_menus() {
  register_nav_menus(
    array(
      'header-menu' => __( 'Header Menu' ),
      'extra-menu' => __( 'Extra Menu' )
     )
   );
 }
 add_action( 'init', 'register_my_menus' );
 ```

Выводим меню
`wp_nav_menu()`

```
wp_nav_menu( array( 'theme_location' => 'header-menu' ) );
```

# Шаблоны страниц
```
<?php
/*
Template Name: Full-width layout
Template Post Type: post, page, event
*/
// Page code here...
```


# Виджеты

```
<?php
function themename_widgets_init() {
    register_sidebar( array(
        'name'          => __( 'Primary Sidebar', 'theme_name' ),
        'id'            => 'sidebar-1',
        'before_widget' => '<aside id="%1$s" class="widget %2$s">',
        'after_widget'  => '</aside>',
        'before_title'  => '<h1 class="widget-title">',
        'after_title'   => '</h1>',
    ) );

    register_sidebar( array(
        'name'          => __( 'Secondary Sidebar', 'theme_name' ),
        'id'            => 'sidebar-2',
        'before_widget' => '<ul><li id="%1$s" class="widget %2$s">',
        'after_widget'  => '</li></ul>',
        'before_title'  => '<h3 class="widget-title">',
        'after_title'   => '</h3>',
    ) );
}
add_action( 'widgets_init', 'themename_widgets_init' );
```

```
<?php get_sidebar(); ?>
```

```
<?php get_sidebar( 'primary' ); ?>
```

```
<div id="sidebar-primary" class="sidebar">
    <?php if ( is_active_sidebar( 'primary' ) ) : ?>
        <?php dynamic_sidebar( 'primary' ); ?>
    <?php else : ?>
        <!-- Time to add some widgets! -->
    <?php endif; ?>
</div>
```
