# TraversyMediaTutorial-NestJS-Crash-Course

[Tutorial](https://www.youtube.com/watch?v=wqhNoDE6pb4)
from [Traversy Media YouTube channel](https://www.youtube.com/user/TechGuyWeb)

# Notes

When I was following the tutorial I was facing with the next issue:

> Nest can't resolve dependencies of the ItemsService (?). Please make sure that the argument at index [0] is available
> in the AppModule context.

In order to solve it you have to remove the ItemsController and ItemsService imports from the `app.module.ts` file.

This was the solution because:

1. You already import ItemsController and ItemsService in your `items.module.ts` file so it's not necessary to import
them again in the `app.module.ts` file.
2. In your `items.module.ts` you have the next line:
    ```typescript
    @Module({
      imports: [MongooseModule.forFeature([{ name: 'Item', schema: ItemSchema }])],
      ...
    })
    ```
    which is necessary to make the dependency injection in the `items.service.ts` file works, as you can check in the
    `app.module.ts` file you don't have that line.
3. Of course you can add that line to your `app.module.ts` file but then there's no sense to create the
`items.module.ts` file.
