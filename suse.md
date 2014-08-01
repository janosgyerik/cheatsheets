Create user, with home directory, and member of `users` group:

    useradd -m -G users janos

Add user to `wheel` group:

    usermod -G wheel janos

Both in one step:

    useradd -m -G users,wheel janos
