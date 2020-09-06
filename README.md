# Recaptcha-bundle


I created this Bundle for educational purposes, with Symfony 5, to be able to share my services with other developers. 
However this Bundle is functional, you can use it, and allows you to add a Recaptcha v2 invisible from google in your forms !

## Install the package with:

```console
composer require mdoutreluingne/recaptcha-bundle
```

And... that's it! If you're *not* using Symfony Flex, you'll also
need to enable the `mdoutreluingne\RecaptchaBundle\RecaptchaBundle`
in your `config/bundles.php` file. Like this :

```bundles
mdoutreluingne\RecaptchaBundle\RecaptchaBundle::class => ['all' => true]
```

## Usage

This bundle provides a service to generate a submit button with 
recaptcha v2 invisible from google using `RecaptchaSubmitType` type-hint in your class Type:

```php
// src/Form/UnknownType.php

use mdoutreluingne\RecaptchaBundle\Type\RecaptchaSubmitType;
// ...

class UnknownType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            // ...
            ->add('captcha', RecaptchaSubmitType::class, [
                'label' => 'Submit',
                'attr' => [
                    'class' => 'btn btn-primary'
                ]
            ])
        ;
    }
    
    // ...
}
```

## Configuration

You need to create and configure the `recaptcha.yaml` file in config/packages like this:

```yaml
# config/packages/recaptcha.yaml
recaptcha:
  key: '%env(GOOGLE_RECAPTCHA_KEY)%'
  secret: '%env(GOOGLE_RECAPTCHA_SECRET)%'
```
And after that, integrate your key and google secret vote in the file `.env`
