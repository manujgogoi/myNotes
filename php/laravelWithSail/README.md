```bash
curl -s "https://laravel.build/example-app" | bash

cd example-app

./vendor/bin/sail up

./vendor/bin/sail artisan migrate
```

Finally, you can access the application in your web browser at: `http://localhost`.
