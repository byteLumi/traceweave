# Runtime Settings

The pipeline uses low reasoning effort with a logical deadline of 600 seconds for experience-organization calls and 1,500 seconds for distillation, at most three transport attempts, and an executor timeout of 7,200 seconds per instance. Retries apply only to transport failures and never change the verdict of a valid trial that failed the verifier.
