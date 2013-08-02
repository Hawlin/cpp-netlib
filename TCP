// Copyright (c) 2012 A. Linunix (linunixinception@gmail.com).
// Distributed under the Boost Software License, Version 1.0.
// (See accompanying file LICENSE_1_0.txt or copy at
// http://www.boost.org/LICENSE_1_0.txt)

#ifndef SYN_CNNECT_HPP
#define SYN_CNNECT_HPP

#include <boost/asio/ip/tcp.hpp>
#include <boost/system/error_code.hpp>
#include <boost/asio.hpp>

#include <chrono> // later
#include <functional>
#include <utility>
#include <iostream>
#include <mutex> // later

using namespace boost;

namespace boost { namespace network { namespace TCP {

class syn_cnnect
{
    
public:

    syn_cnnect(asio::io_service & io) : sock(io) { }

public:

    void connect(const std::string &host, unsigned short port, system::error_code & erc)
    {
        if(!erc)
           sock.connect(asio::ip::tcp::endpoint(
                     asio::ip::address::from_string(host), port));
                     
        else
            std::cout << "The TCP Connexion was failed, try again" << std::endl;
            sock.shutdown(boost::asio::ip::tcp::socket::shutdown_both);
    }
    
    void connect_end(asio::ip::tcp::endpoint & end)
    {
       sock.connect(end);
    }

    void connect_v4(const std::string  &host, unsigned short port, system::error_code & erc)
    {
        if(!erc)
          sock.connect(boost::asio::ip::tcp::endpoint(
                       boost::asio::ip::address_v4::from_string(host), port));

          boost::asio::detail::throw_error(erc);
    }

    void connect_v6(const std::string &host , unsigned short port, system::error_code & erc)
    {
        if(!erc)
           sock.connect(boost::asio::ip::tcp::endpoint(
                      boost::asio::ip::address_v6::from_string(host), port));

        else
          std::cout << "Failed to connected" << std::endl;
          sock.shutdown(boost::asio::ip::tcp::socket::shutdown_both);
    }

    void cancel ()
    {
        sock.cancel();
    }

    void close ()
    {
        sock.close();
    }

    ~syn_cnnect()
    {
        sock.shutdown(boost::asio::ip::tcp::socket::shutdown_both);
        sock.close();
    }

private:

    boost::asio::ip::tcp::socket sock;

};

} } }

#endif // SYN_CNNECT_HPP
