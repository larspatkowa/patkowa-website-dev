<script>
    import { page } from '$app/stores';
    $: fullMessage = $page.status === 404 ? `${$page.status}: page not found` :
                      $page.status === 500 ? `${$page.status}: internal server error` :
                      String($page.status);

    let index = 0;
    let increasing = true;
    $: message = fullMessage.substring(0, index) || '\u00A0';
    let blink = true;

    function typeWriter() {
        if (increasing) {
            if (index < fullMessage.length) {
                index++;
            } else {
                setTimeout(() => {
                    increasing = false;
                    index--;
                }, 2000);
                 // Exit the function to wait for the timeout
            }
        } else {
            if (index >= 0) {
                index--;
            } else {
                increasing = true;
                index++;
            }
        }
        message = fullMessage.substring(0, index);
    }

    const interval = setInterval(typeWriter, 100);
    const blinkInterval = setInterval(() => {
        blink = !blink;
    }, 500);
</script>

<div class="fixed inset-0 flex items-center justify-center">
    <h1 class="text-[36px] font-medium typing text-cream border-r-4 text-grey-40 pr-0.5 pt-1 border-cream min-w-1 border-transparent leading-none" class:border-transparent={!blink}>{message}</h1>
</div>
