function toString(encoding, start, end) {
  if (arguments.length === 0) {
    return this.utf8Slice(0, this.length);
  }

  const len = this.length;

  if (start <= 0)
    start = 0;
  else if (start >= len)
    return '';
  else
    start |= 0;

  if (end === undefined || end > len)
    end = len;
  else
    end |= 0;

  if (end <= start)
    return '';

  if (encoding === undefined)
    return this.utf8Slice(start, end);

  const ops = getEncodingOps(encoding);
  if (ops === undefined)
    throw new ERR_UNKNOWN_ENCODING(encoding);

  return ops.slice(this, start, end);
}