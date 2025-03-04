# AI SDK - LangDB.ai Provider

The **[LangDB provider](https://sdk.vercel.ai/providers/ai-sdk-providers/langdb)** for the [AI SDK](https://sdk.vercel.ai/docs) contains language model support for the [LangDB AI Gateway](https://langdb.ai) platform.

## Setup

The LangDB provider is available in the `langdb/vercel-provider` module. You can install it with

```bash
npm i langdb/vercel-provider
```

## Provider Instance


```ts
import { createLangDB } from 'langdb/vercel-provider';
import { v4 as uuidv4 } from 'uuid';

const langDB = createLangDB(
  apiKey: 'your_api_key',
  projectId: 'your_project_id',
  threadId: uuidv4(),
  runId: uuidv4(),
  label: 'scientist',
);

```

## Example

### Generating Text

You can generate text using LangDB.ai models:

```ts
import { createLangDB } from 'langdb/vercel-provider';
import { generateText } from 'ai';

const langDB = createLangDB(
  apiKey: 'your_api_key',
  projectId: 'your_project_id',
  threadId: uuidv4(),
  runId: uuidv4(),
  label: 'scientist',
);

const { text } = await generateText({
  model: langDB('openai/gpt-4o-mini'),
  prompt: 'Write a Python function that sorts a list:',
});

console.log(text);
```

### Generating Images

You can also generate images using LangDB.ai's image models:

```ts
import { experimental_generateImage as generateImage } from 'ai';
import fs from 'fs';
import path from 'path';

const { images } = await generateImage({
  model: langDB.image('openai/dall-e-3'),
  prompt: 'A delighted resplendent quetzal mid-flight amidst raindrops',
});

const imagePath = path.join(__dirname, 'generated-image.png');
fs.writeFileSync(imagePath, images[0].uint8Array);
console.log(`Image saved to: ${imagePath}`);
```

### Creating Text Embeddings

You can also generate text embeddings

```ts
import { embed } from 'ai';

const { embedding } = await embed({
  model: langDB.textEmbeddingModel('text-embedding-3-small'),
  value: 'sunny day at the beach',
});

console.log('Embedding:', embedding);
```

## Documentation

Please check out the **[LangDB provider Documentation](https://docs.langdb.ai/guides/vercel-ai-sdk)** for more information.
