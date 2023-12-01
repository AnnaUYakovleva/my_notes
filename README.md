Если большинство столбцов являются числовыми, возможно, имеет смысл просто try это сделать и пропустить столбец, если это не работает:

for column in df.columns:
    try:
        df[column] = np.log10(df[column])
    except (ValueError, AttributeError):
        pass
Конечно, если вы хотите, вы могли бы обернуть это в функцию.

Если все столбцы числовые, вы даже можете просто выполнить

df_log10 = np.log10(df)

Вы можете использовать select_dtypes и numpy.log10:

import numpy as np
for c in df.select_dtype(include = [np.number]).columns:
    df[c] = np.log10(df[c])
