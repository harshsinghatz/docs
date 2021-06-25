---
id: usage
title: How to use
hide_title: true
---

# How to use

## Use the override config: [API Reference](/docs/nodejs/emailpassword/override/functions)

<!--DOCUSAURUS_CODE_TABS-->
<!--NodeJS-->
```js
SuperTokens.init({
    appInfo: {...},
    supertokens: {...},
    recipeList: [
        EmailPassword.init({
__HIGHLIGHT__            override: {
                functions: (originalImplementation) => {
                    return {
                        ...originalImplementation,
                        signUp: async (input) => {
                            // TODO: some custom logic

                            // or call the default behaviour as show below
                            return await originalImplementation.signUp(input);
                        },
                        // ...
                        // TODO: override more functions
                    }
                },
                emailVerificationFeature: {
                    functions: (originalImplementationEmailVerification) => {
                        return {
                            ...originalImplementationEmailVerification,
                            isEmailVerified: async (input) => {
                                // TODO: some custom logic

                                // or call the default behaviour as show below
                                return await originalImplementationEmailVerification.isEmailVerified(input);
                            },
                            // ...
                            // TODO: override more functions
                        }
                    }
                }
            } __END_HIGHLIGHT__
        })
    ]
});
```
<!--END_DOCUSAURUS_CODE_TABS-->

- `originalImplementation` and `originalImplementationEmailVerification` are objects that contains functions that have the original implementation for this and the email verification recipe. They can be used in your functions as a way to use the SuperTokens' default behaviour.
- In the above code snippet, we override the `signUp` function of this recipe. This function will be used to handle the scenario when the user clicks on the sign up button from the frontend.
- Likewise, we override the `isEmailVerified` function for the email verification recipe.