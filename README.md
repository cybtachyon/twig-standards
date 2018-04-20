# Twig Style Guide

*A mostly reasonable approach to Twig*

This is a superset of the [Official SensioLabs Twig Standards](http://twig.sensiolabs.org/doc/coding_standards.html).

It should be compatible with the [Drupal Twig Coding Standards](https://www.drupal.org/node/1823416).

Very heavily 'inspired' by [airbnb/Javascript](https://github.com/airbnb/javascript).

## Table of Contents

  1. [Tags](#tags)
  1. [Filters](#filters)
  1. [Functions](#functions)
  1. [Tests](#tests)
  1. [Operators](#operators)
  1. [Variables](#variables)
  1. [Blocks](#blocks)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Commas](#commas)
  1. [Naming Conventions](#naming-conventions)
  1. [Resources](#resources)
  1. [In the Wild](#in-the-wild)
  1. [Translation](#translation)
  1. [Contributors](#contributors)

## Tags

**[⬆ back to top](#table-of-contents)**

## Filters

<a name="replace-string-tokens"><a name="2.1"></a>
  - [2.1]() String tokens to be used inside the `replace` filter should be
    marked with percentage signs.

    ```twig
    {# Bad. #}
    {{ sidekicks|replace('{{ robin }}', 'Dick Grayson') }}

    {# Good. #}
    {{ sidekicks|replace('%robin%', 'Jason Todd') }}
    ```

**[⬆ back to top](#table-of-contents)**

## Functions

**[⬆ back to top](#table-of-contents)**

## Tests

**[⬆ back to top](#table-of-contents)**

## Operators

**[⬆ back to top](#table-of-contents)**

## Variables

**[⬆ back to top](#table-of-contents)**

## Blocks

<a name=""></a><a name="7.1"></a>
  - [7.1]() Blocks that span multiple lines should have their opening and
    closing tags on their own lines.

    ```twig
    {# Bad. #}
    {% include '@components/component.image.twig' with {
      'src' = image.src,
      'alt' = image.alt,
      'attributes' = image.attributes,
      'sources' = image.sources,
    } only %}


    {# Good. #}
    {%
    include '@components/component.image.twig' with {
      'src' = image.src,
      'alt' = image.alt,
      'attributes' = image.attributes,
      'sources' = image.sources,
    } only
    %}

    {# Bad. #}
    {% set hero = {
      'firstName': 'Florence',
      'lastName': 'Nightingale',
      'inventorOf': ['coxcomb chart', 'modern nursing'],
    } %}

    {# Good. #}
    {%
    set hero = {
      'firstName': 'Florence',
      'lastName': 'Nightingale',
      'inventorOf': ['coxcomb chart', 'modern nursing'],
    }
    %}


    {# Bad. #}
    {{ foo
      |replace({ '_': ' ' })
      |title
      |default('foo') }}

    {# Good. #}
    {{
    foo
      |replace({ '_': ' ' })
      |title
      |default('foo')
    }}
    ```

**[⬆ back to top](#table-of-contents)**

## Comments

**[⬆ back to top](#table-of-contents)**

## Whitespace

  <a name="whitespace--spaces"></a><a name="9.1"></a>
  - [9.1](#whitespace--spaces) Use soft tabs set to 2 spaces.

    ```twig
    {# Bad. #}
    {%
    set foo = [
    ∙∙∙∙name
    ]
    %}

    {# Bad. #}
    {%
    set foo = [
    ∙name
    ]
    %}

    {# Good. #}
    {%
    set baz = [
    ∙∙name;
    ]
    %}
    ```

  <a name="whitespace--before-blocks"></a><a name="9.2"></a>
  - [9.2](#whitespace--before-blocks) Place 1 space before the leading brace.

    ```twig
    {# Bad. #}
    {%
    set dog={
      'age': '1 year',
      'breed': 'Bernese Mountain Dog',
    }
    %};

    {# Good. #}
    {%
    set dog = {
      'age': '1 year',
      'breed'': 'Bernese Mountain Dog',
    }
    %};
    ```

  <a name="whitespace--around-keywords"></a><a name="9.3"></a>
  - [9.3](#whitespace--around-keywords) Place 1 space before the opening
    parenthesis in control statements (`if`, `for` etc.). Place no space
    between the argument list and the function name in function calls and
    declarations.

    ```twig
    {# Bad. #}
    {% if(isJedi) %}
      {% set enemy = 'sith' %}
    {% endif %}

    {# Good. #}
    {% if (isJedi) %}
      {% set enemy = 'sith' %}
    %}

    {# Bad. #}
    {{ jedi|default ('Yoda') }}

    {# Good. #}
    {{ jedi|default('Yoda') }}
    ```

  <a name="whitespace--infix-ops"></a><a name="9.4"></a>
  - [9.4](#whitespace--infix-ops) Set off operators with spaces.

    ```twig
    {# Bad. #}
    {% set x=y+5 %}

    {# Good. #}
    {% set x = y + 5 %}
    ```

  <a name="whitespace--newline-at-end"></a><a name="9.5"></a>
  - [9.5](#whitespace--newline-at-end) End files with a single newline
    character.

    ```twig
    {# Bad. #}
    {{ stuff }}
    ```

    ```twig
    {# Bad. #}
    {{ stuff }}↵
    ↵
    ```

    ```twig
    {# Good. #}
    {{ stuff }}↵
    ```

  <a name="whitespace--chains"></a><a name="9.6"></a>
  - [9.6](#whitespace--chains) Use indentation when making long filter chains
    (more than 2 filter chains). Use a leading dot, which emphasizes that the
    line is a method call, not a new statement.

    ```twig
    {# Bad. #}
    {{ foo|upper|lower|title|default('foo') }}

    {# Bad. #}
    {{
    foo|
      upper|
      lower|
      title|
      default('foo')
    }}

    {# Good. #}
    {{
    foo
      |upper
      |lower
      |title
      |default('foo')
    }}

    {# Bad. #}
    {{
    foo|upper
      |lower|title
      |default('foo')
    }}

    {# Good. #}
    {{ foo|title|default('foo') }}
    ```

  <a name="whitespace--padded-blocks"></a><a name="9.7"></a>
  - [9.7](#whitespace--padded-blocks) Do not pad your blocks with blank lines.

    ```twig
    {# Bad. #}
    {%

      set foo = 'bar'

    %}

    {# Bad. #}
    {% if baz %}

      {{ qux }}
    {% elseif %}
      {{ foo }}

    {% endif %}

    {# Good. #}
    {%
    set foo = 'bar'
    %}

    {# Good. #}
    {% if baz %}
      {{ qux }}
    {% elseif %}
      {{ foo }}
    {% endif %}
    ```

  <a name="whitespace--in-parens"></a><a name="9.8"></a>
  - [9.8](#whitespace--in-parens) Do not add spaces inside parentheses.

    ```twig
    {# Bad. #}
    {{ foo|default( 'foo' ) }}

    {# Good. #}
    {{ foo|default('foo') }}
    ```

  <a name="whitespace--in-brackets"></a><a name="9.9"></a>
  - [9.9](#whitespace--in-brackets) Do not add spaces inside brackets.

    ```twig
    {# Bad. #}
    {% set foo = [ 1, 2, 3 ] %}
    {{ foo.0 }}

    {# Good. #}
    {% set foo = [1, 2, 3] %}
    {{ foo.0 }}
    ```

  <a name="whitespace--in-braces"></a><a name="9.10"></a>
  - [9.10](#whitespace--in-braces) Add spaces inside curly braces.

    ```twig
    {# Bad. #}
    {% set foo = {clark: 'kent'} %}

    {# Good. #}
    {% set foo = { clark: 'kent' } %}
    ```

  <a name="whitespace--max-len"></a><a name="9.11"></a>
  - [9.11](#whitespace--max-len) Avoid having lines of code that are longer than
    80 characters (including whitespace).

    > Why? This ensures readability and maintainability.

    ```twig
    {# Bad. #}
    {% set foo = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.' %}

    {# Bad. #}
    {% if victory|default %}{{ congratulations }}{% else %}{{ failure }}{% endif %}

    {# Good. #}
    {%
    set foo = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed ' ~
      'do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
    %}

    {# Good. #}
    {% if victory|default %}
      {{ congratulations }}
    {% else %}
      {{ failure }}
    {% endif %}
    ```

**[⬆ back to top](#table-of-contents)**

## Commas

<a name="commas--leading-trailing"></a><a name="10.1"></a>
  - [10.1](#commas--leading-trailing) Leading commas: **No.**

    ```twig
    {# Bad. #}
    {%
    set story = [
      'once'
    , 'upon'
    , 'a'
    , 'time'
    ]
    %}

    {# Good. #}
    {%
    set story = [
      once,
      upon,
      aTime,
    ];
    %}

    {# Bad. #}
    {%
    set hero = {
        'firstName': 'Ada'
      , 'lastName': 'Lovelace'
      , 'birthYear': '1815'
      , 'superPower': 'computers'
    }
    %}

    {# Good. #}
    {%
    set hero = {
      'firstName': 'Ada',
      'lastName': 'Lovelace',
      'birthYear': '1815',
      'superPower': 'computers',
    %}
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [10.2](#commas--dangling) Additional trailing comma: **Yes.**

    > Why? This leads to cleaner git diffs.

    ```twig
    {# Bad. Git diff. #}
    {%
    set hero = {
         'firstName': 'Florence',
    -    'lastName': 'Nightingale'
    +    'lastName': 'Nightingale',
    +    'inventorOf': ['coxcomb chart', 'modern nursing']
    }
    %}

    {# Good. Git diff. #}
    {%
    set hero = {
         'firstName': 'Florence',
         'lastName': 'Nightingale',
    +    'inventorOf': ['coxcomb chart', 'modern nursing'],
    }
    %}
    ```

    ```twig
    {# Bad. #}
    {%
    set hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    }
    %}

    {%
    set heroes = [
      'Batman',
      'Superman'
    ]
    %}

    {# Good. #}
    {%
    set hero = {
      'firstName': 'Dana',
      'lastName': 'Scully',
    }
    %}

    {%
    set heroes = [
      'Batman',
      'Superman',
    ]
    %}
    ```

**[⬆ back to top](#table-of-contents)**

## Naming Conventions

**[⬆ back to top](#table-of-contents)**

## Resources

**Tools**

  - [Standalone Twig Linter](https://github.com/asm89/twig-lint)

**[⬆ back to top](#table-of-contents)**

## In the Wild

  - **Mediacurrent**: [Mediacurrent/twig-standards](https://github.com/Mediacurrent/twig-standards)

**[⬆ back to top](#table-of-contents)**

## Translation

  We'd love to have it, so please submit a PR to add your fork in another language!

  - ![ae](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-States.png) **American English**: [cybtachyon/twig-standards](https://github.com/cybtachyon/twig-standards)

## Contributors

- [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)

**[⬆ back to top](#table-of-contents)**
