<!--
SPDX-License-Identifier: GPL-2.0

Verbatim excerpt from Linux kernel Documentation/process/5.Posting.rst,
section "Patch preparation". Source:
https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/plain/Documentation/process/5.Posting.rst
Upstream revision: bd5f485f3f026225b86573e559af0b7254ef4184

The wording below is intentionally preserved from upstream. Do not paraphrase it
when using it as the acceptance criteria for a patch series.
-->

# Ordinary contributor patch-series requirements

Only the most simple changes should be formatted as a single patch;
everything else should be made as a logical series of changes.  Splitting
up patches is a bit of an art; some developers spend a long time figuring
out how to do it in the way that the community expects.  There are a few
rules of thumb, however, which can help considerably:

 - The patch series you post will almost certainly not be the series of
   changes found in your working revision control system.  Instead, the
   changes you have made need to be considered in their final form, then
   split apart in ways which make sense.  The developers are interested in
   discrete, self-contained changes, not the path you took to get to those
   changes.

 - Each logically independent change should be formatted as a separate
   patch.  These changes can be small ("add a field to this structure") or
   large (adding a significant new driver, for example), but they should be
   conceptually small and amenable to a one-line description.  Each patch
   should make a specific change which can be reviewed on its own and
   verified to do what it says it does.

 - As a way of restating the guideline above: do not mix different types of
   changes in the same patch.  If a single patch fixes a critical security
   bug, rearranges a few structures, and reformats the code, there is a
   good chance that it will be passed over and the important fix will be
   lost.

 - Each patch should yield a kernel which builds and runs properly; if your
   patch series is interrupted in the middle, the result should still be a
   working kernel.  Partial application of a patch series is a common
   scenario when the "git bisect" tool is used to find regressions; if the
   result is a broken kernel, you will make life harder for developers and
   users who are engaging in the noble work of tracking down problems.

 - Do not overdo it, though.  One developer once posted a set of edits
   to a single file as 500 separate patches - an act which did not make him
   the most popular person on the kernel mailing list.  A single patch can
   be reasonably large as long as it still contains a single *logical*
   change.

 - It can be tempting to add a whole new infrastructure with a series of
   patches, but to leave that infrastructure unused until the final patch
   in the series enables the whole thing.  This temptation should be
   avoided if possible; if that series adds regressions, bisection will
   finger the last patch as the one which caused the problem, even though
   the real bug is elsewhere.  Whenever possible, a patch which adds new
   code should make that code active immediately.

Working to create the perfect patch series can be a frustrating process
which takes quite a bit of time and thought after the "real work" has been
done.  When done properly, though, it is time well spent.
