# Hamming

Что делает:

- использует результат из ноутбука `huffman/sample_compression.ipynb`;
- берет сжатый Хаффманом поток из `data/huffman_block_1.bin`;
- берет таблицу декодирования из `data/huffman_block_1.json`;
- защищает битовый поток кодом Хэмминга `(7,4)`;
- пропускает поток через канал, где каждый бит искажается с вероятностью `3%`;
- пытается восстановить исходный поток и текст;
- выводит, сколько ошибок осталось после декодирования.

## Локальный запуск

Из корня проекта:

```bash
uv sync
uv run jupyter notebook hamming/error_correcting.ipynb
```

Текст уже должен лежать в:

```text
data/brothers_karamazov.txt
```

Перед запуском этого ноутбука нужно выполнить `huffman/sample_compression.ipynb`, чтобы появились:

```text
data/huffman_block_1.bin
data/huffman_block_1.json
```

После запуска дополнительно сохраняются:

```text
data/hamming_protected.bin
data/hamming_protected.json
data/hamming_noisy.bin
data/hamming_noisy.json
data/hamming_restored_huffman.bin
data/hamming_restored_huffman.json
```

`hamming_restored_huffman.bin` — это результат попытки восстановления после Хэмминга. При битовой вероятности ошибки `3%` в одном 7-битном блоке иногда бывает больше одной ошибки, поэтому обычный Хэмминг `(7,4)` не гарантирует полное восстановление.
